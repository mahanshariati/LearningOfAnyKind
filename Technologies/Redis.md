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

It is possible to flag a specific client connection to be excluded from the client eviction mechanism. 
If, for example, you have an application that monitors the server via the INFO command and alerts you in case of a problem, you might want to make sure this connection isn't evicted.
- You can do so using the following command (from the relevant client's connection): CLIENT NO-EVICT on
- And you can revert that with: CLIENT NO-EVICT off

## Client Timeouts
By default recent versions of Redis don't close the connection with the client if the client is idle for many seconds: the connection will remain open forever. \\
However if you don't like this behavior, you can configure a timeout, so that if the client is idle for more than the specified number of seconds, the client connection will be closed.



