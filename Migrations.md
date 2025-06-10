# DB Migrations in ASP.NET Core

Migrations are a code-based way to:
- Create the database schema from C# classes (models).
- Update the database schema when your models change — without deleting existing data.
- Basically, track all DDL changes in your data models.

## 🔄 The Migration Flow (Simple Version)

- We have an initial model, that we created the first time.

```csharp
public class User {
    public int Id { get; set; }
    public string Name { get; set; }
}
```
- We do migration

```bash
dotnet ef migrations add InitialCreate
```

- EF tries to compares this new model with a previous model,but finds nothing, Thus, establishes that this is the initial migration
- Then it creates a C# file `InitialCreate.cs` in Migrations/       these files contain two methods usually, `Up()` (to apply changes) and `Down()` (to revert those changes)

```csharp
migrationBuilder.CreateTable(
    name: "Users",
    columns: table => new {
        Id = table.Column<int>(nullable: false)
            .Annotation("SqlServer:Identity", "1, 1"),
        Name = table.Column<string>(nullable: true)
    });
```

- NOW, EF takes a snapshot of our updated model and saves a file called `ModelSnapshot.cs`
- This snapshot is used next time to detect what changed.
- EF basically takes snapshot after each migration.
  
- It then executes these pending changes against our database on `dotnet ef database update` and finalizes everything.

---

- Now if we update something:

```csharp
  public class User {
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }  // 👈 new property
}
```

```bash
dotnet ef migrations add AddEmailToUser
```

EF:
- Looks at current model
- Looks at `ModelSnapshot`
- Detects new `Email` Property
- Generates migration file for it:

```csharp
migrationBuilder.AddColumn<string>(
    name: "Email",
    table: "Users",
    nullable: true);
```

- Now agian we do: `dotnet ef database update`
- EF executes the migrations against our database by converting all these instructions to SQL

---

### Remove 
- The `dotnet ef migrations remove` command removes the most recent migration that has not yet been applied to the database.
- Use this when:
    - You made a mistake in your model.
    - You ran add migration too early.
    - You want to clean up your source code and EF's internal state
    - **You haven’t run update-database yet** (i.e., migration isn’t applied to the DB).
- THis command only deletes the last pending migrations files and its accompanying .Designer.cs file (in older versions of asp.net, it only contained some metadata)
- And the migration file is then reverted to the previous migration state
- It DOES NOT revert changes in your model classes, those should be manually removed or fixed.
- It DOES NOT undo applied migrations in the database, those should also be manually handled.

---

# Common Commands

| Command                           | What It Does                                       |
| --------------------------------- | -------------------------------------------------- |
| `dotnet ef migrations add <Name>` | Create a new migration based on model changes      |
| `dotnet ef database update`       | Apply all pending migrations to the DB             |
| `dotnet ef migrations remove`     | Remove the last created migration (if not applied) |
| `dotnet ef migrations list`       | See all migration names                            |
| `dotnet ef database drop`         | Delete the database                                |
