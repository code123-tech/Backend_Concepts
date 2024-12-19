Partitioning of data into multiple DB shards (instances). which is kind of Horizontal scaling of the DB.
One of the strategy **consistent hashing** can be used to perform sharding.

###### chart
1. No split data, No sharding  -> Single DB instances with no partitioning
2. Split Data, No sharding     ->  Single db instance but data is splitted
3. No split Data, sharding.    ->.  Multiple DB instance, exact replication of previous data into new DB instance. Master-follower kind of architecutre
4. Split Data, sharding        ->.  Multiple DB instance, with splitted data across those instances.

