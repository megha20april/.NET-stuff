# 🌱 What Is Seeding Data?

Seeding means pre-populating your database with initial data when the database is created or updated.
Think of it like:

> "Planting default values into your tables" 🌱

## 🧠 Why Use Seeding?

- Add default roles like "Admin", "User".
- Add sample products, countries, categories, etc.
- Ensure the app works right away after DB setup — no need to manually insert values.


>  Since, this is seeding data, meaning adding data at the time of db's creation,
> these changes are included in migration files.
>
> If you include or change seed data, EF treats it like a schema change and generates a new migration.


## 🧱 How do we do this?

#### 1. Through `OnModelCreating()` method

- It is a virtual method in DbContext class meaning it can be overridden.
- EF Core calls this method when it builds the model metadata — i.e., when it’s figuring out how your C# classes map to DB tables.
- You override it in your subclass of DbContext to inject custom configuration or seed data.
- Since we know that after each request, the DbContext is disposed and a new one is created, so whatever we add in this method will be executed every time a new DbContext is created.
- It takes a `ModelBuilder` parameter

##### ModelBuilder Class
- this object basically is used to build a IModel object (an immutable, compiled, read-only structure) that contains all the configurations in which our c# classes are mapped to our database.

- for ex: 
    - when we create a DbSet entity, It tells EF that this is a table in the database.
    - and it then registers the entity type with the model builder like this:

    ```csharp
        modelBuilder.Entity<User>()
        .ToTable("AppUsers")
        .HasIndex(u => u.Email)
        .IsUnique();
    ```
    - So, we can also use this explicit way to register entities to the model builder.
    - After all this config is done, we call `modelBuilder.FinalizeModel()` to finalize the model, and it returns an IModel object. which is then used by EF Core to perform database operations through our classes.
 
- Now each entity in modelBuilder has a `.HasData()` method, which tells EF to add the defined records into the entity when first initializing it.
