### Q: What is SQL Server?

> SQL Server is Microsoft’s relational database management system (RDBMS) used to store, manage, and retrieve data efficiently. It uses T-SQL (Transact-SQL) for querying and supports transactions, stored procedures, and indexing.

### Q: What is the difference between CHAR and VARCHAR?

> CHAR(n) stores fixed-length strings (always uses n bytes).  
> VARCHAR(n) stores variable-length strings (uses only needed space).  
> Use CHAR for consistent-length codes (like country codes) and VARCHAR for general text.

### Q: What is a Stored Procedure?

> A Stored Procedure is a precompiled SQL statement that can be executed with parameters.

```sql
CREATE PROCEDURE GetOrdersByStudent
  @StudentID INT
AS
SELECT * FROM Orders WHERE StudentID = @StudentID;
```

### Q: What is an Index?

> An index improves query performance by allowing faster data retrieval, similar to a book’s index.

### Q: What is a View?

> A View is a virtual table created from a query result.

### Q: What are the ACID properties in SQL Server?

> **Atomicity:** All operations in a transaction succeed or fail together.
> **Consistency:** Database moves from one valid state to another.
> **Isolation:** Concurrent transactions don’t affect each other.
> **Durability:** Once committed, data is permanent.

### Q: What is the difference between INNER JOIN, LEFT JOIN, and FULL JOIN?

> **INNER JOIN:** Returns only matching rows.  
> **LEFT JOIN:** Returns all rows from the left table + matches.  
> **FULL JOIN:** Returns all rows from both tables.

### Q: How do you prevent SQL injection in SQL Server?

> Use parameterized queries or stored procedures instead of dynamic SQL.

```sql
cmd.CommandText = "SELECT * FROM Users WHERE Username = @name";
cmd.Parameters.AddWithValue("@name", username);
```

### Q: What are clustered and non-clustered indexes?

> Clustered Index: Defines the physical order of data (1 per table).  
> Non-Clustered Index: A separate structure with pointers to data rows.

### Q: What is a Transaction and how do you use it?

> A transaction ensures a group of operations are treated as one logical unit.

```sql
BEGIN TRANSACTION
UPDATE Accounts SET Balance -= 100 WHERE Id = 1;
UPDATE Accounts SET Balance += 100 WHERE Id = 2;
COMMIT TRANSACTION;
```

### Q: How does SQL Server handle deadlocks?

> A deadlock occurs when two transactions block each other. SQL Server detects it automatically and terminates one (the “victim”).  
> Prevention: Access resources in a consistent order and keep transactions short.

### Q: How do you improve query performance in SQL Server?

> Add appropriate indexes  
> Use SELECT with needed columns only  
> Avoid SELECT \*  
> Use query execution plans to find bottlenecks  
> Instead of:  
> SELECT \* FROM Orders;  
> Use:  
> SELECT OrderID, StudentID FROM Orders;
