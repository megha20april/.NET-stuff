# Entity Framework Core

- It is designed to work with .NET Core and .NET Framework applications and provides an Object-Relational Mapper (ORM) that enables .NET developers to work with a database using .NET objects. It eliminates most of the data-access code that developers usually need to write.

## What is ORM?

- ORM stands for Object-Relational Mapping, a programming technique that allows developers to convert data between incompatible systems, specifically between Object-Oriented Programming Languages (such as C#, Java, etc.) and Relational Databases (such as SQL Server, MySQL, Oracle, etc.).
- ORM allows developers to work with data in terms of objects rather than tables and columns. That means ORM automatically creates classes based on database tables, and vice versa is also true. It can also generate the necessary SQL to create the database based on the classes.
- It can generate the necessary SQL (to perform the database CRUD operation) that the underlying database can understand.
- It takes responsibility for opening the connection, executing the command, handling the transaction to ensure data integrity, closing the connection, etc.

## What happens if we don't use an ORM?

Without using an ORM Framework like Entity Framework or EF Core, we have to write lots of data access code to perform the CRUD operations, i.e., store and retrieve the Student, Department, and Address data from the underlying database tables.

For example, to perform CRUD operations, i.e., read, insert, update, or delete from a database table, we generally need to write the required SQL statements, which the underlying database should understand.

Again, when we want to read the data from the database into our application, we also have to write some custom logic to map the data to our model classes like Student, Department, Address, etc. This is a common task that we do in almost every application.

An ORM Framework like Entity Framework or EF Core can do all of the above for us and saves a lot of time if we provide the required information to the ORM Framework. The ORM Framework sits between our application code and the Database. It eliminates the need for most custom data-access codes we usually write without an ORM

## Entity Framework Core Development Approaches:

- Code-First Approach: In this approach, the data model (classes) is created first, and Entity Framework Core generates the database schema based on the model.
- Database-First Approach: This approach is used when an existing database is available. Entity Framework Core can generate the data model (classes) based on the database schema.

___


## DbContextOptions
- this is a class that builds our options object which is used to set the configurations for our DbContext, to connect it to our database.
- It basically tells the DbContext all the useful configs used to connect to our db.
- This options object is then passed to the constructor of DbContext, to bind that config object to that specific context.
- this object also contains the db provider specific configurations.

- Now when we instantiate this options object, why do we need to pass a Context type to it? (why is the constructor generic? what special does it do after knowing the particular context type)
- it is used for compile-time error checking and thus ensures type safety. It ensures that we don't end up passing the wrong options object to a context (when we have multiple contexts in our application). Because each options object has provider-specific configs, that might break the connection in another DbContext. It saves runtime errors.
