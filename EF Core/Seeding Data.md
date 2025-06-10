# 🌱 What Is Seeding Data?

Seeding means pre-populating your database with initial data when the database is created or updated.
Think of it like:
> "Planting default values into your tables" 🌱

## 🧠 Why Use Seeding?

- Add default roles like "Admin", "User".
- Add sample products, countries, categories, etc.
- Ensure the app works right away after DB setup — no need to manually insert values.


> Since, this is seeding data, meaning adding data at the time of db's creation, these changes are included in migration files.
> If you include or change seed data, EF treats it like a schema change and generates a new migration.

## 🧱 How do we do this?

#### 1. Through `OnModelCreating()` method

- It is a special method in DbContext class.
