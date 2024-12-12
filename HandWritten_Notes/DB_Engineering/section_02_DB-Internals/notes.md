###### Tables and Indexes stored on Disk
* **Logical Table:** representation of data being stored in form of rows.
* **Row_Id:** each row of table has some unique id to fetch the row data, In MySQL it is primary key whereas in PostgreSQL, it creates system column row_id.
* **Page:** An area in the memory where rows of table are stored. a page can have more than one rows. DB doesn't read a single row instead of it reads page or pages with un-necessary rows. Page size: 8KB (In Postgres), 16KB(In MySQL)
* **IO (Input/Output):** read request to the disk, helps to fetches pages of the query we executed. try to minimize this as much as possible.
* **Heap:** data structure where all the pages of table are being stored. traversing a heap to fetch a row data is costly and time consuming, that is why indexes helps to fetch exactly the part of heap we need to read.
* **Index:** another data structure that has pointer to heap entries. Indexing can be done on one or more columns.

###### Note
* Primary key considered as clustered index unless specified. 
* MySQL Innodb have primary key as clustered index and other index (secondary indexes) point to primary key 
* In Postgres, row_id is clustered index, and all other user defined index are secondary indexes which point to row_id

###### Row v/s Column oriented Databases
Row and Column oriented Databases are two storage stypes which DB use to storage their data of table on disk.
* **Row oriented Databases:** 
  * Tables are stored as rows in disk. In single IO, you fetches multiple rows with all their columns due to Page
  * It's a useful when it is needed to read all columns or certain columns of fetched results.
  * It's not useful when performing aggregation on particular column. Ex: calculating sum(salary) of all the employees, it will pull all columns of all rows and then find salary from each row.
* **Column oriented Databases:**
  * Tables are stored as columns of table in disk. In single IO, you fetches multiple columns with all matching rows.
  * This is useful only if less columns are being fetched in a query, for ex: Aggregation. It will take Less IO operations.
  * But on fetching more columns of matching rows, It will take High IOs for ex: select * from <Table>