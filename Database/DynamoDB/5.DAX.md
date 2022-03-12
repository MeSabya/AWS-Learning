- DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performance improvement – from milliseconds to microseconds – even at millions of requests per second.
- DAX is intended for high-performance reads application. As a write-through cache, DAX writes directly so that the writes are immediately reflected in the item cache.
- DAX as a managed service handles the cache invalidation, data population, or cluster management.
- DAX saves cost reducing the read load (RCU) on DynamoDB
- DAX helps prevent hot partitions
- DAX only supports eventual consistency, and strong consistency requests are passed-through to DynamoDB.
- DAX is fault-tolerant and scalable.
- DAX cluster has a primary node and zero or more read-replica nodes. Upon a failure for a primary node, DAX will automatically fail over and elect a new primary. For scaling, add or remove read replicas.
- DAX supports server-side encryption.
- DAX does not support Transport Layer Security (TLS).

## DynamoDB Accelerator Operations

### Eventual Read operations

If DAX has the item available (a cache hit), DAX returns the item without accessing DynamoDB.

If DAX does not have the item available (a cache miss), DAX passes the request through to DynamoDB. When it receives the response from DynamoDB, DAX returns the results to the application. But it also writes the results to the cache on the primary node.

Strongly Consistent Read operations

DAX passes the request through to DynamoDB. The results from DynamoDB are not cached in DAX. but simply returned

### For Write operations

Data is first written to the DynamoDB table, and then to the DAX cluster.

Operation is successful only if the data is successfully written to both the table and to DAX.

## DynamoDB Accelerator Caches

DAX cluster has two distinct caches – Item cache and Query cache

### Item cache
Item remains in the DAX item cache, subject to the Time to Live (TTL) setting and the least recently used (LRU) algorithm for the cache
DAX provides write-through cache, keeping the DAX item cache consistent with the underlying DynamoDB tables.

### Query cache
DAX caches the results from Query and Scan requests in its query cache
Query and Scan results don’t affect the item cache at all, as the result set is saved in the query cache – not in the item cache.
Writes to Item cache don’t affect the Query cache

## DynamoDB Accelerator Write Strategies

1. Write-Through
2. Write-Around


