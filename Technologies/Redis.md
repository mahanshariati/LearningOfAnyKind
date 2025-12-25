# Redis – Caching, Persistence, and Messaging

## Client Eviction
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

## Client Timeouts
By default recent versions of Redis don't close the connection with the client if the client is idle for many seconds: the connection will remain open forever. <br>
However if you don't like this behavior, you can configure a timeout, so that if the client is idle for more than the specified number of seconds, the client connection will be closed.
- You can configure this limit via redis.conf or simply using CONFIG SET timeout <value>.
- Note that the timeout only applies to normal clients and it does not apply to Pub/Sub clients, since a Pub/Sub connection is a push style connection so a client that is idle is the norm.
<br>
Timeouts are not to be considered very precise: Redis avoids setting timer events or running O(N) algorithms in order to check idle clients, so the check is performed incrementally from time to time. This means that it is possible that while the timeout is set to 10 seconds, the client connection will be closed, for instance, after 12 seconds if many clients are connected at the same time.

## The CLIENT Command 
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




