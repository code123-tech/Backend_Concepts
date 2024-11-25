**Transaction:** Collection of sequential queries, treated as one unit of work. Ex: Transfer of money from an account to another.

**_Transaction LifeSpan_**
1. **BEGIN:** Start of the transaction.
2. **COMMIT:** End of the transaction. Changes are made permanent.
3. **ROLLBACK:** End of the transaction. Changes are discarded.

Below is not considered, just a state.
1. Unexpected Ending = ROLLBACK (eg: Crash)

**_ACID Properties_**
1. **Atomicity (A):** 
   * All queries must succeed, even one query fails txn should rollback.
   * Even, DB goes down prior to commit, Txn should be rollback.
   * Lack of atomicity leads to inconsistency.

2. **Consistency (C):** 
   * DB should be in a consistent state before and after the transaction.
   * Constraints, Triggers, etc. should be maintained.
   * Consistency in data
     * Defined by user
     * Referential Integrity
     * Atomicity
     * Isolation
   * Consistency in reads
     * Eventual Consistency: Once the data is at two places (cache and actual DB), you might get inconsistency.
       Both Relational and NoSQL suffers from this situation, when we want to scale horizontally or introduce caching.

3. **Isolation (I):** An In-flight transaction should not consume changes made by other in-flight transaction in the same time.
    * Read Phenomena
      1. **Dirty Reads:** T1 transaction tries to read the data of DB which are uncommitted by T2 transaction.
      2. **Non-Repeatable Reads:** When you read something, and tries to read same value again that committed by other Txn.
      3. **Phantom Reads:** You have some range query (like date query), now T1 insert a row and do not commit that change and you do a range query. Now, you get that inserted row also which is uncommitted.
      4. **Lost Updates:** T1 lost its updates as some other txn overrides your changes.
   * Isolation Levels
     1. **Read Uncommitted:** no isolation, read committed or uncommitted changes by outside txn.
     2. **Read committed:** T1 queries sees only committed changes of other transaction.
     3. **Repeatable read:** to prevent Non-repeatable reads, if query with values are read by T1, that remains unchanged during complete txn T1.
     4. **Snapshot:** Each query in txn only sees changes that have been committed upto the start of the txn It's like snapshot version of the DB (Costly)
     5. **Serializable:** Txn are run as they serialized one after the other.
   * Each DB implements Isolation levels differently.
   * [Database System](https://en.wikipedia.org/wiki/Isolation)
   * DB Implementation of isolation:
     1. **Pessimistic:** Row level locks, table locks, page locks to avoid lost updates.
     2. **Optimistic:** No locks, just track the changes at the end of txn, if things changed or not fail the txn
     3. **Repeatable Read:** It locks the rows which can be expensive if read a lot of rows, postgres implements RR as snapshot.
     4. **Serializable:** are usually implemented with optimistic concurrency control.

4. **Durability:** Anything which is being written by client in some non-volatile storage system, 
   It means it should always be available to the client even power is lost or crash happens. 
   * Durability techniques:
     * WAL - Write Ahead Logging: Writing a lot of data to disk, but it is expensive. DBMSs persist a compressed version of changes known as Write ahead log segments.
     * Asynchronous snapshot: As we write, keep everything in memory and asynchronously write to disk. Redis uses both current and above concept for durability
     * Append only file (AOF)

**Os Cache**
* Write request in OS usually goes to the OS cache, and sends signal that write is completed. In BG, it creates batches and flushes data into disk, 
  but what before flush OS crashes.
* As per user, commit is done, but it is not actually done because OS cache did not perform disk flush due to crash.
* Most of DBs suffer from this problem but this is very rare case.
* can override this situation using `Fsync` OS command to directly flush to disk, but it will be very slow and expensive to be used.


**Command to set isolation level in Postgres**

    BEGIN transaction isolation level <isolation_level>


