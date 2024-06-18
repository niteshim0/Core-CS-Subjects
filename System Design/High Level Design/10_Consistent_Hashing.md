 **Consistent Hashing** is a distributed hashing scheme that operates independently of the number of servers or objects in a distributed hash table by assigning them a position on an abstract circle, or hash ring. This allows servers and objects to scale without affecting the overall system.

# Why Consistent Hashing is Needed ?

Sharding is a good enough strategy but it has quite a few limitations:

`Resharding data`: Resharding data is needed when 
1. a single shard could no longer hold more data due to rapid growth. 
2. Certain shards might experience shard exhaustion faster than others due to uneven data distribution. When shard exhaustion happens, it requires updating the sharding function and moving data around. Consistent Hashing is used to resolve this, which needs an article on its own.


`Celebrity problem`: Excessive access to a specific shard could cause server overload. Imagine data for Messi, CR7, and Neymar all end up on the same shard. For social applications, that shard will be overwhelmed with read operations. To solve this problem, we may need to allocate a shard for each celebrity. Each shard might even require further partition.

This article explains consistent hashing beautifully [A Guide to Consistent Hashing](https://www.toptal.com/big-data/consistent-hashing)