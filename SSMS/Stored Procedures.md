# Stored Procedures in SQL Server Management Studio (SSMS)

- Stored procedures are precompiled collections of SQL statements that can be executed as a single unit.
- They can accept parameters, return results, and encapsulate complex logic.
- These are just a way to group SQL statements together for easier management and execution and promote code reuse.

> can be found under the "Programmability" section in the Object Explorer of SSMS.

# System Stored Procedures

- these are present by default and are provided by microsoft 
- these are provided to help with common tasks like creating, modifying, and deleting objects in the database or managing security and permissions

# User-Defined Stored Procedures

- these are created by users to encapsulate custom logic and business rules

# Creating a Stored Procedure 

- can be created by typing in New Query window in SSMS and executing the SQL code or by right-clicking on the "Stored Procedures" node in the Object Explorer and selecting "New Stored Procedure".

### `<procedure_name>` naming convention

- `<owner_name>` is the the database owner ex. `dbo` (default owner in SQL Server)
- `sp` is a common prefix used to indicate that the object is a stored procedure, but it is not mandatory.
- But make sure not to use the `sp_` prefix for user-defined stored procedures, as it is reserved for system stored procedures.
- `<primary_table_name>` is the name of the primary table that the stored procedure will interact with. We could be using multiple tables, but this is the main one.
- `<Functionality>` describes the purpose or functionality of the stored procedure, such as `Insert`, `Update`, `Delete`, or `GetData`.

example: `dbo.spEmployee_Insert` etc.


```sql
CREATE PROCEDURE <owner_name>.sp<primary_table_name>_<Functionality>
AS
BEGIN
    -- SQL statements go here
END;
```


# Executing a Stored Procedure

- can be executed using the `EXEC` or `EXECUTE` command followed by the procedure name and any required parameters.

```sql
EXEC <procedure_name>
```
- inside any query window in SSMS.

# Output of Stored Procedure

- The output of a stored procedure can be in the form of result sets, Output Parameter, messages, or return values.
- Result sets are the most common output, which can be viewed in the Results tab of SSMS. They are basically table-like structures.
- Return values are typically used to indicate the success or failure of the procedure, often represented by an integer value. 
    - For example, a return value of 0 might indicate success, while any other value indicates an error or specific condition.
- Output parameters are variables you define outside the procedure and the procedure modifies their value and sends them back.
- Messages can be printed using the `PRINT` statement within the procedure, which will appear in the Messages tab of SSMS. or they can include things like no. of rows affected, warnings, and information (like "Command completed successfully") etc.
     - No. of rows affected means how many rows were inserted, updated, or deleted by the procedure.
     - In a SELECT statement, it indicates how many rows were returned by the query.


The Messages tab in SSMS displays these messages, including any output from the PRINT statement, the number of rows affected, and any warnings or errors that occurred during execution.

### SET NOCOUNT ON

These no. of rows affected messages are often disabled by `SET NOCOUNT ON` statement, which is commonly used in stored procedures to prevent these messages from being returned. Each message takes a small amount of memory and network bandwidth. Hence disabling them can improve performance by avoiding unnecessary messages in the output when running large queries or procedures.


# Altering a Stored Procedure

- altering a SP means modifying its definition, which can be done using the `ALTER PROCEDURE` statement followed by the procedure name and the new definition.

# Parameters in Stored Procedures

- Parameters are used to pass values into the stored procedure, allowing it to operate on dynamic data.
- Example of a stored procedure with parameters:

```sql
CREATE PROCEDURE <owner_name>.sp<primary_table_name>_<Functionality>
    @Parameter1name INT,
    @Parameter2name VARCHAR(50)
AS
```
- then in the body of the procedure, you can use these parameters like variables:

```sql
BEGIN
    SELECT * FROM <primary_table_name> WHERE Column1 = @Parameter1name AND Column2 = @Parameter2name;
END;
```
- When executing the procedure, you can pass values to these parameters:

```sql
EXEC <owner_name>.sp<primary_table_name>_<Functionality> @Parameter1name = 1, @Parameter2name = 'example';

-- or
EXEC <owner_name>.sp<primary_table_name>_<Functionality> 1, 'example';  -- if the order of parameters is known
```

# Trancations in Stored Procedures

- A transaction is a set of operations that are treated as a single unit. They either all succeed (commit) or all fail (rollback).
- Transactions help maintain data integrity and consistency.

Syntax:

```sql
BEGIN TRANSACTION;
-- SQL commands here
COMMIT;
-- or ROLLBACK;
```

# Error Handling in Stored Procedures

```sql
BEGIN TRY
    BEGIN TRANSACTION;
    -- SQL commands
    COMMIT;
END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT ERROR_MESSAGE();
END CATCH
```