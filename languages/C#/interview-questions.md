### Q: What is C#?

> C# is a modern, object-oriented programming language developed by Microsoft as part of the .NET framework. It combines the power of C++ with the simplicity of Visual Basic, and is used for developing web, desktop, and cloud applications.

### Q: What is the .NET Framework?

> The .NET Framework is a development platform created by Microsoft that provides a controlled programming environment for building and running applications. It includes:
>
> - CLR (Common Language Runtime): manages code execution
> - BCL (Base Class Library): provides reusable classes and APIs

### Q: What is CLR in .NET?

> The Common Language Runtime (CLR) is the virtual machine component of .NET that manages code execution. It handles:
>
> - Memory management (Garbage Collection)
> - Type safety
> - Exception handling
> - Thread management

### Q: What are Value Types and Reference Types in C#?

```csharp
int x = 10;          // Value type
string name = "Bob"; // Reference type
```

> **Value Types:**
>
> - Stored on stack
> - Contains actual data
> - Copied when assigned
> - Examples: int, struct, enum, bool, DateTime
> - Default value when null
>
> **Reference Types:**
>
> - Stored on heap
> - Contains reference to data
> - Reference copied when assigned
> - Examples: class, string, array, delegate
> - Can be null

### Q: What is the difference between == and .Equals() in C#?

> == compares reference equality for reference types and value equality for value types.
>
> .Equals() can be overridden to define custom equality logic.
>
> **== operator:**
>
> > - Reference comparison for reference types (by default)
> > - Value comparison for value types
> > - Can be overloaded
> > - Static method
>
> **Equals():**
>
> > - Virtual method from Object
> > - Can be overridden
> > - Handles null safely
> > - Default: reference comparison
> > - For strings: both compare values Always override both together for custom types

### Q: What is a Namespace in C#?

> A namespace organizes related classes and avoids naming conflicts.

```csharp
namespace MyApp.Models {
    class User { }
}
```

### Q: What is the difference between const and readonly in C#?

> const → compile-time constant
>
> readonly → value assigned at runtime (e.g., in constructor)

```csharp
const double Pi = 3.14;
readonly string Name;
```

### Q: What is Boxing and Unboxing in C#?

> Boxing: Converting a value type to an object Unboxing: Extracting the value type from an object

```csharp
int x = 10;
object obj = x;       // Boxing
int y = (int)obj;     // Unboxing
```

### Q: What are Access Modifiers in C#?

> **Access modifiers define visibility:**
>
> - public — accessible everywhere
> - private — accessible only within class
> - protected — accessible in derived classes
> - internal — accessible within same assembly

### Q: What is the difference between var, dynamic, and explicit typing?

var is compile-time safe, dynamic is flexible but slower.

```csharp
var name = "Tom";      // Inferred at compile-time
dynamic data = 123;    // Type checked at runtime
string city = "Sydney";// Explicit typing

```

### Q: What are Properties in C#?

Properties are members that provide controlled access to class fields.

```csharp
class Person {
    public string Name { get; set; }
}
```

### Q: What is the difference between an Abstract Class and an Interface?

| Feature        | Abstract Class            | Interface                                                   |
| -------------- | ------------------------- | ----------------------------------------------------------- |
| Implementation | Can contain method bodies | Cannot contain implementations (until C# 8 default methods) |
| Inheritance    | Only one allowed          | Multiple allowed                                            |
| Fields         | Can have fields           | Cannot have fields                                          |

### Q: What is LINQ in C#?

LINQ (Language Integrated Query) allows querying collections or databases in a readable syntax.

```csharp
var result = from n in numbers
             where n > 5
             select n;
```

### Q: What is Entity Framework Core?

EF Core is an ORM (Object-Relational Mapper) for .NET that allows developers to interact with databases using C# classes instead of SQL queries.

```csharp
var students = context.Students.Where(s => s.Age > 20).ToList();
```

> **Tracking:**
>
> > - Tracks changes to entities retrieved from context
> > - Enables automatic SaveChanges updates
> > - Uses more memory
>
> **AsNoTracking:**
>
> > - Read-only queries
> > - Better performance
> > - Lower memory usage
> > - Use for read-only scenarios

### Q: What is the difference between StringBuilder and String?

> **String:**
>
> > - Immutable
> > - Each operation creates new object
> > - Inefficient for multiple concatenations
> > - Thread-safe by nature
>
> **StringBuilder:**
>
> > - Mutable
> > - Modifies same instance
> > - Efficient for multiple operations
> > - Not thread-safe
> > - Use when doing 5+ string operations

### Q: What is the difference between FirstOrDefault and SingleOrDefault?

> **FirstOrDefault:**
>
> > - Returns first element or default
> > - Doesn't check if more elements exist
> > - More performant
> > - Use when multiple matches are acceptable
>
> **SingleOrDefault:**
>
> > - Returns single element or default
> > - Throws if multiple elements exist
> > - Less performant (checks entire sequence)
> > - Use when expecting exactly 0 or 1 match

### Q: What is the purpose of the var keyword in C#?

> var allows the compiler to infer the variable’s type at compile time. It keeps code clean but still strongly typed.

```csharp
var name = "Oliver"; // string
var count = 10;      // int
```

### Q: What is a constructor in C#?

> A constructor is a special method called when an object is created. It initializes fields.

```csharp
public class Car {
    public string Model;
    public Car(string model) {
        Model = model;
    }
}
```

### Q: What is the difference between public and private?

> public members are accessible anywhere, while private members are only accessible inside the same class.
>
> Encapsulation encourages making fields private and exposing only necessary properties or methods.

### Q: What is a static class?

> A static class cannot be instantiated. All members must be static. Often used for helpers or utility functions.
>
> Example: Math class.

### Q: What is method overloading?

> Method overloading means multiple methods with the same name but different parameters.

```csharp
void Log(string msg)
void Log(string msg, int level)
```

### Q: What is the difference between List<T> and an array (T[])?

> Arrays are fixed-size; List is dynamic and can grow or shrink.
>
> I prefer List for most business scenarios due to flexibility.

### Q: What is an enum?

> An enum is a named set of constant values—useful for statuses and categories.

```csharp
public enum OrderStatus { Pending, Paid, Cancelled }
```

### Q: What is string interpolation?

> Using $"" to embed variables inside a string.

```csharp
var name = "Tom";
Console.WriteLine($"Hello {name}");
```

### Q: What is the difference between int and int??

> int cannot be null; int? (nullable int) can store null. Useful when reading optional database values.

### Q: What is the default value of a class field?

> - Reference types default to null.
> - Numeric value types default to 0.
> - Booleans default to false.

### Q: What is the difference between foreach and for?

> foreach iterates through collections without indexing, while for uses an index and is better when you need index values or want to modify the list.
>
> foreach is also safer because it prevents out-of-range errors.

### Q: What does the virtual keyword do?

> It allows a method to be overridden in derived classes.

```csharp
public virtual void Speak() { }
```

### Q: What does override mean in C#?

> override replaces a base class’s virtual method with a new implementation.

```csharp
public override void Speak() {
    Console.WriteLine("Dog barking");
}
```

### Q: What is the purpose of the ?? operator?

> Null-coalescing operator: returns a fallback value when the left side is null.

```csharp
string result = input ?? "default";
```
