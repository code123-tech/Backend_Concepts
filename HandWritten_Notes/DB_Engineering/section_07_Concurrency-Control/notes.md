**Exclusive Lock:** Acquiring lock on a row such that no other transaction can edit it when you are editing it.

**Shared Lock:** Acquiring lock on a row such that no other transaction can edit it when you are reading it. 

This locks are useful in various systems ex: Banking system. You need consistency at every moment in those systems, but due to this various transaction might suffer failure.

**Note:** 
T1 has taken exclusive lock on row of table A, T2 now can't take both exclusive and shared lock on that row. It has to wait for T1 to release the lock.

T1 has taken shared lock on a row of table A, T2 now can't take exclusive, but can take shared lock on the same row of table A.


###### Understand 2-Phase Locking
* https://www.youtube.com/watch?v=1pUaEDNLWi4
* Drawbacks: https://www.youtube.com/watch?v=pZExswIjVsk