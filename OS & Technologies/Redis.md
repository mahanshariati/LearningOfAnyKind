# Redis – Caching, Persistence, and Messaging
- [Redis – Caching, Persistence, and Messaging](#redis--caching-persistence-and-messaging)
  - [commands](#commands)
    - [String commands](#string-commands)
    - [Hash commands](#hash-commands)
    - [List commands](#list-commands)
    - [Sorted set commands](#sorted-set-commands)
    - [Pub/Sub commands](#pubsub-commands)
    - [Generic commands ](#generic-commands-)
  - [Client Handling](#client-handling)
    - [Client Eviction](#client-eviction)
    - [Client Timeouts](#client-timeouts)
    - [The CLIENT Command](#the-client-command)
    - [TCP Keepalive](#tcp-keepalive)
    - [Client Tools](#client-tools)
  - [go-redis](#go-redis)
    - [Production usage](#production-usage)
      - [Error Handling](#error-handling)
        - [Applying error handling patterns](#applying-error-handling-patterns)
      - [Health Check](#health-check)
      - [Retries](#retries)
      - [Timeouts](#timeouts)
      - [Example of configuring Client](#example-of-configuring-client)


## commands
### [String commands](https://redis.io/docs/latest/commands/redis-8-4-commands/#string-commands)
- [APPEND](https://redis.io/commands/append/) - Appends a string to the value of a key. Creates the key if it doesn't exist.
- [GET](https://redis.io/commands/get/) - Returns the string value of a key.
- [MGET](https://redis.io/commands/mget/) - Atomically returns the string values of one or more key
- [SET](https://redis.io/commands/set/) - Sets the string value of a key, ignoring its type. The key is created if it doesn't exist.
- [MSET](https://redis.io/commands/mset/) - Atomically creates or modifies the string values of one or more keys.

### [Hash commands](https://redis.io/docs/latest/commands/redis-8-4-commands/#hash-commands)
- [HGET](https://redis.io/commands/hget/) - Returns the value of a field in a hash.
- [HMGET](https://redis.io/commands/hmget/) - Returns the values of all fields in a hash.
- [HSET](https://redis.io/commands/hset/) - Creates or modifies the value of a field in a hash.
- [HMSET](https://redis.io/commands/hmset/) - Sets the values of multiple fields.
- [HDEL](https://redis.io/commands/hdel/) - Deletes one or more fields and their values from a hash. Deletes the hash if no fields remain.
- [HEXPIRE](https://redis.io/commands/hexpire/) - Set expiry for hash field using relative time to expire (seconds)

### [List commands](https://redis.io/docs/latest/commands/redis-8-4-commands/#list-commands)
### [Sorted set commands](https://redis.io/docs/latest/commands/redis-8-4-commands/#sorted-set-commands)
### [Pub/Sub commands](https://redis.io/docs/latest/commands/redis-8-4-commands/#pubsub-commands)
### [Generic commands ](https://redis.io/docs/latest/commands/redis-8-4-commands/#generic-commands)


## Client Handling
### Client Eviction
Redis is built to handle a very large number of client connections. Client connections tend to consume memory, and when there are many of them, the aggregate memory consumption can be extremely high, leading to data eviction or out-of-memory errors.
client eviction is essentially a safety mechanism that will disconnect clients once the aggregate memory usage of all clients is above a threshold. 
- The mechanism first attempts to disconnect clients that use the most memory. 
- It disconnects the minimal number of clients needed to return below the maxmemory-clients threshold.
- maxmemory-clients defines the maximum aggregate memory usage of all clients connected to Redis.
- The aggregation takes into account all the memory used by the client connections: the query buffer, the output buffer, and other intermediate buffers.
- Note that replica and master connections aren't affected by the client eviction mechanism. Therefore, such connections are never evicted.
- maxmemory-clients can be set permanently in the configuration file (redis.conf) or via the CONFIG SET command. 
- This setting can either be 0 (meaning no limit), a size in bytes (possibly with mb/gb suffix), or a percentage of maxmemory by using the % suffix (e.g. setting it to 10% would mean 10% of the maxmemory configuration).
- The default setting is 0, meaning client eviction is turned off by default.

It is possible to flag a specific client connection to be excluded from the client eviction mechanism. <br>
If, for example, you have an application that monitors the server via the INFO command and alerts you in case of a problem, you might want to make sure this connection isn't evicted.
- You can do so using the following command (from the relevant client's connection): CLIENT NO-EVICT on
- And you can revert that with: CLIENT NO-EVICT off

### Client Timeouts
By default recent versions of Redis don't close the connection with the client if the client is idle for many seconds: the connection will remain open forever. <br>
However if you don't like this behavior, you can configure a timeout, so that if the client is idle for more than the specified number of seconds, the client connection will be closed.
- You can configure this limit via redis.conf or simply using CONFIG SET timeout <value>.
- Note that the timeout only applies to normal clients and it does not apply to Pub/Sub clients, since a Pub/Sub connection is a push style connection so a client that is idle is the norm.
<br>
Timeouts are not to be considered very precise: Redis avoids setting timer events or running O(N) algorithms in order to check idle clients, so the check is performed incrementally from time to time. This means that it is possible that while the timeout is set to 10 seconds, the client connection will be closed, for instance, after 12 seconds if many clients are connected at the same time.

### The CLIENT Command 
The Redis CLIENT command allows you to inspect the state of every connected client, to kill a specific client, and to name connections. It is a very powerful debugging tool if you use Redis at scale.<br>
CLIENT LIST is used in order to obtain a list of connected clients and their state:
```bash
redis 127.0.0.1:6379> client list
addr=127.0.0.1:52555 fd=5 name= age=855 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 events=r cmd=client
addr=127.0.0.1:52787 fd=6 name= age=6 idle=5 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 events=r cmd=ping
```


- addr: The client address, that is, the client IP and the remote port number it used to connect with the Redis server.
- fd: The client socket file descriptor number.
- name: The client name as set by CLIENT SETNAME.
- age: The number of seconds the connection existed for.
- idle: The number of seconds the connection is idle.
- flags: The kind of client (N means normal client, check the full list of flags).
- omem: The amount of memory used by the client for the output buffer.
- cmd: The last executed command.

### TCP Keepalive
From version 3.2 onwards, Redis has TCP keepalive (SO_KEEPALIVE socket option) enabled by default and set to about 300 seconds. This option is useful in order to detect dead peers (clients that cannot be reached even if they look connected). Moreover, if there is network equipment between clients and servers that need to see some traffic in order to take the connection open, the option will prevent unexpected connection closed events.

### Client Tools
- The [redis-cli](https://redis.io/docs/latest/develop/tools/#redis-command-line-interface-cli) command line tool
- [Redis Insight](https://redis.io/docs/latest/develop/tools/#redis-insight) (a graphical user interface tool)
- The Redis [VSCode extension](https://redis.io/docs/latest/develop/tools/#redis-vscode-extension)
- Redis in Database section of Goland




## go-redis
This guide summarizes the [go-redis](https://redis.io/docs/latest/develop/clients/go/) section in Redis docs, explains how to install go-redis and connect your application to a Redis database. It also offers recommendations to get the best reliability and performance in your production environment. 
for knowing how to configure the client for connection to redis checkout [Example of configuring Client](#example-of-configuring-client)

### Production usage
The sections below offer recommendations for your production environment.

#### Error Handling
go-redis uses explicit error returns following Go's idiomatic error handling pattern.

```Go
result, err := rdb.Get(ctx, key).Result()
if err != nil {
    // Handle the error
}
```

| Error | When it occurs | Recommended action |
|-------|----------------|--------------------|
| redis.Nil | Key does not exist | Return default value or fetch from source |
| context.DeadlineExceeded | Operation timeout | Retry with backoff |
| net.OpError | Network error | Retry with backoff or fall back to alternative |
| redis.ResponseError | Redis error response | [NOT RECOVERABLE] Fix the command or arguments |


##### Applying error handling patterns
- Pattern 1: Fail fast (return the error): <br>
   - Use this when the error is unrecoverable or indicates a bug in your code.

- Pattern 2: Graceful degradation (Check for specific errors and fall back to an alternative database): <br>
    - Use this when you have an alternative way to get the data you need, so you can fall back to using the alternative instead of the preferred code. for example: <br> 
      - Cache reads (fallback to database)
      - Session reads (fallback to default values)
      - Optional data (skip if unavailable)

- Pattern 3: Retry with backoff (Retry on temporary errors such as timeouts): <br>
    - Use this when the error could be due to network load or other temporary conditions. for example:
        - Connection timeouts
        - Temporary network issues
        - Redis loading data
    
    ```Go
    import time

    max_retries = 3
    retry_delay = 0.1

    for attempt in range(max_retries):
        try:
            return r.get(key)
        except redis.TimeoutError:
            if attempt < max_retries - 1:
                time.sleep(retry_delay)
                retry_delay *= 2  # Exponential backoff
            else:
                raise
    ```

    - Note that client libraries often implement retry logic for you.

- Pattern 4: Log and continue (Log non-critical errors and continue): <br>
    - Use this when the operation is not critical to your application. for example:
        - Cache writes (data loss is acceptable)
        - Non-critical updates
        - Metrics collection

#### Health Check
If your code doesn't access the Redis server continuously then it might be useful to make a "health check" periodically (perhaps once every few seconds). You can do this using a simple PING command:
```Go
err := rdb.Ping(ctx).Err()

if err != nil {
  // Report failed health check.
}
```

#### Retries
- go-redis will automatically retry failed connections and commands. 
- By default, the number of attempts is set to three, but you can change this using the MaxRetries field of Options when you connect. 
- The retry strategy starts with a short delay between the first and second attempts, and increases the delay with each attempt.

#### Timeouts
- go-redis supports timeouts for connections and commands to avoid stalling your app if the server does not respond within a reasonable time.
- The DialTimeout field of Options sets the timeout for connections, and the ReadTimeout and WriteTimeout fields set the timeouts for reading and writing data, respectively.

#### Example of configuring Client
client:
```Go
func New(cfg *config.RedisConfig, logger logger.Logger) (*redis.Client, error) {
    var tlsConfig *tls.Config
    opts := &redis.Options{
        Addr:            cfg.Hosts[0],
        Username:        cfg.Username,
        Password:        cfg.Password,
        Protocol:        cfg.Protocol,
        MaxRetries:      cfg.MaxRetries,
        MinRetryBackoff: cfg.MinRetryBackoff,
        MaxRetryBackoff: cfg.MaxRetryBackoff,
        DialTimeout:     cfg.DialTimeout,
        ReadTimeout:     cfg.ReadTimeout,
        WriteTimeout:    cfg.WriteTimeout,
    }
    if tlsConfig != nil {
        opts.TLSConfig = tlsConfig
    }
    rcc := redis.NewClient(opts)
    return rcc, nil
}
```

client for cluster:
```Go
func New(cfg *config.RedisConfig, logger logger.Logger) (*redis.ClusterClient, error) {
    var tlsConfig *tls.Config
    opts := &redis.Cluster{
        Addrs:           cfg.Hosts,
        Username:        cfg.Username,
        Password:        cfg.Password,
        Protocol:        cfg.Protocol,
        MaxRetries:      cfg.MaxRetries,
        MinRetryBackoff: cfg.MinRetryBackoff,
        MaxRetryBackoff: cfg.MaxRetryBackoff,
        DialTimeout:     cfg.DialTimeout,
        ReadTimeout:     cfg.ReadTimeout,
        WriteTimeout:    cfg.WriteTimeout,
    }
    if tlsConfig != nil {
        opts.TLSConfig = tlsConfig
    }
    rcc := redis.NewClusterClient(opts)
    return rcc, nil
}
```



