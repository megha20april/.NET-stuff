In C#, a **static constructor** is a special type of constructor used to initialize **static members** of a class **only once**, before the class is used for the first time.

---

### 🔧 Key Points:

* It **cannot take parameters** since as it's a first thing called, there is no way we can pass anything to it.
* It **cannot be called explicitly**.
* It is **called automatically** by the CLR **before any static members are accessed** or the class is instantiated.
* A class **can have only one static constructor**.

---

### 🧱 Syntax:

```csharp
class MyClass
{
    static MyClass()
    {
        // Initialization logic
        Console.WriteLine("Static constructor called");
    }
}
```

---

### 🧠 When Is It Called?

* When the class is **accessed for the first time**, either:

  * A static member is accessed.
  * An instance of the class is created.

---

### 📌 Example:

```csharp
class Example
{
    public static int StaticValue;

    static Example()
    {
        StaticValue = 42;
        Console.WriteLine("Static constructor executed");
    }

    public Example()
    {
        Console.WriteLine("Instance constructor executed");
    }
}
```

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine(Example.StaticValue); // Triggers static constructor
        var obj = new Example();               // Triggers instance constructor
    }
}
```

**Output:**

```
Static constructor executed  
42  
Instance constructor executed
```

---

### 🛑 Notes:

* You can't define a static constructor with `public`, `private`, or any access modifier. It is **always private** by default.
* It's used commonly for **logging setups**, **static configuration**, **singleton initialization**, etc.

### More Examples

```csharp
class Example
{
    public static int StaticValue;

    static Example()
    {
        Console.WriteLine("Static constructor executed");
    }

    static public Main()
    {
        Console.WriteLine("main entry point");
    }
}
```

**Output:**

```
Static constructor executed  
main entry point
```
the entry point is main, but before executing the logic inside main, the control jumps to static constructor and executes it afterwhich it comes back to main function.
