# System Design

## Object-Oriented Programming (OOP) Principles
OOP is constructed over 4 major principles: **EAPI (Encapsulation, Abstraction, Polymorphism, Inheritance)**.

### Encapsulation
Encapsulation is about **information hiding**. An object has to provide its users only with the essential information for manipulation, without the internal details.

Encapsulation is implemented by using **access specifiers**. An access specifier defines the scope and visibility of a class member. There are 5 access specifiers in C#.

 - **Public Access Specifier**
   
   Allow a class to expose its member variables and methods to other methods and objects.
   
 - **Private Access Specifier**
   
   Allow a class to hide its member variables and methods from other methods and objects. Only methods of the same class can access its private members.
   
 - **Protected Access Specifier**
 
   Allow a child class to access the member variables and methods of its base class.
   
 - **Internal Access Specifier**
 
   Allow a class to expose its member variables and methods to other methods and objects in the same namespace/assembly.
 
 - **Protected Internal Access Specifier**
 
   Allow a class to hide its member variables and methods from other methods and objects, except a child class within the same namespace.assembly.
   
### Abstraction
Abstraction is about **working with thing that we know how to use without knowing how it works internally**.

Encapsulation is used to hide its members from outside class or interface, whereas abstraction is used to show only essential features.

#### Abstract Classes
Abstract classes are place holders for actual implementation classes. Hence, if a class is an abstract class, we cannot create an instance of that class.

The abstract class **defines behavior**, and the subclasses **implement that behavior**.

```
public abstract class Product
{
  ...
}
```

An abstract class is **only to be inherited from**. The advantage is that it enforces certain hierarchies for all the subclasses. It is a kind of contract that **forces all the subclasses to carry on the same hierarchies or standards**.

#### Interfaces
Interface is not a class. An interface has **no implementation**; it only has the **signature**. Similar to abstract class, it is also a contract that is used to define **hierarchies for all subclasses** or it defines **specific set of methods and their arguments**.

Coding to an interface, rather than to an implementation, makes our software easier to extend. By coding to an interface, our code will work with all of the interface's subclasses-even ones that **haven't been created yet**.

```
public interface ISupplier
{
  ...
}
```

#### Abstract Classes and Interfaces
When we create an abstract class, we are creating a base class that might have one ore more **completed** methods but at least one or more methods are left uncompleted and declared `abstract`. If all the methods of an abstract class are uncompleted, then it is same as an interface.

When we create an interface, we are creating a set of methods without any implementation that must be overridden by the implemented classes.

The main differences between abstract class and interface is that a class can implement more than one interface but can only inherit from one abstract class.

### Polymorphism
Polymorphism is about **"one interface, multiple functions"**.

Polymorphism can be static or dynamic.

#### Static Polymorphism: Method Overloading

We can have multiple definitions for the same method name in the same scope. The definition of the method must differ from each other by the signature of the method.

```
class PrintData
{
  void Print(int i)
  {
    Console.WriteLine($"I have a number {i}.");
  }
  
  void Print(string s)
  {
    Console.WriteLine($"I have a string {s}.");
  }
}
```

#### Static Polymorphism: Operator Overloading
We can redefine or overload most of the built-in operators available in C# using the keyword **operator**.

```
public static BookingItem operator+ (BookingItem a, BookingItem b)
{
  return new BookingItem 
  {
    ItemDescription = $"{a.ItemDescription}, {b.ItemDescription}",
    SubTotal = a.SubTotal + b.SubTotal
  };
}
```

#### Dynamic Polymorphism
Dynamic polymorphism is implemented by **abstract** classes and **abstract** or **virtual** methods.

Abstract methods do not provide an implementation and **forces** the derived classes to overried the method.

```
class Animal
{
  ...
  
  public abstract void MakeSound();
}

class Bird : Animal
{
   ...
   
   public override void MakeSound()
   {
     Console.WriteLine("Tweet!");
   }
}
```

The virtual method could be implemented differently in different inherited class and the call to these methods will be decided at runtime.

```
public class Animal
{
  ...
  
  public virtual void MakeSound()
  {
    Console.WriteLine("Err...");
  }
}

public class Bird : Animal
{
   ...
   
   public override void MakeSound()
   {
     Console.WriteLine("Tweet!");
   }
}
```

### Inheritance
Inheritance is about **is-kind-of relationship**.

```
public class Animal
{
  public Animal()
  {
    ...
  }
}

public class Bird : Animal
{
  public Bird() : base()
  {
    ...
  }
}
```

The **base** keyword indicates that the base class must be used and allows access to its non-abstract methods via **base.Method(...)**, its member variables via **base.field**, and its constructors via **base(...)**.

## Aggregation
Aggregation is a special form of association, and means that one thing is made up (in part) of another thing.

## Lessons
 - Whenever we find common behavior in two or more places, look to abstract that behavior into a class, and then reuse that behavior in the common classes.
 - We should always favor **coding to the interface, not the implementation**.
 - The easiest way to make our software resilient to change is to make sure **each class has only one reason to change**.
   - When a class has more than one reason to change, it is probably **doing too many things**. Kindly try to break up the functionality into **multiple classes**, where **each individual class does only one thing** -- and therefore has only **one** reason to change.
 
## References
 - [Abstract Class versus Interface](https://www.codeproject.com/Articles/11155/Abstract-Class-versus-Interface)
 - [Chapter 20. Object-Oriented Programming Principles (OOP)](http://www.introprogramming.info/english-intro-csharp-book/read-online/chapter-20-object-oriented-programming-principles)
 - [C# - Encapsulation](https://www.tutorialspoint.com/csharp/csharp_encapsulation.htm)
