###### Definition and types
Partition of data of a table into multiple sub-tables.
1. **Horizontal partitioning:** Slicing table from a range to another range of the given rows. For 100K rows, Partitioning: 1...10k, 10k+1..20k and so on.
2. **Vertical partitioning:** It's a column partitioning, divide the table from multiple columns and reference those sub-tables with a common column.

Horizontal partitioning based on 
1. By Range
2. By List
3. By Hash

###### Horizontal Partitioning v/s Sharding
* HP splits table into sub-tables but those tables are in the same database, client agnostic.
* Sharding splits table into sub-tables but across multiple database servers.

###### Steps to create partition of a table
1. Create a master table first having partition key. (`create table .... partition by RANGE(<column>)`
2. Create all the partition table like the master table which should have partition key.
3. Now, attach all the created partitions to master table.
4. Now describe master table, you will get attached partitions to it
5. Now insert data into master table, it will be automatically distributed among partitions based on `RANGE type`

