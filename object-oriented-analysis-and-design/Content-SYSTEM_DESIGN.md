# System Design

## Abstract Classes
Abstract classes are place holders for actual implementation classes. Hence, if a class is an abstract class, we cannot create an instance of that class.

The abstract class **defines behavior**, and the subclasses **implement that behavior**.

```
public abstract class Product
{
  ...
}
```

An abstract class is **only to be inherited from**. The advantage is that it enforces certain hierarchies for all the subclasses. It is a kind of contract that **forces all the subclasses to carry on the same hierarchies or standards**.

## Interfaces
Interface is not a class. An interface has **no implementation**; it only has the **signature**. Similar to abstract class, it is also a contract that is used to define **hierarchies for all subclasses** or it defines **specific set of methods and their arguments**.

Coding to an interface, rather than to an implementation, makes our software easier to extend. By coding to an interface, our code will work with all of the interface's subclasses-even ones that **haven't been created yet**.

```
public interface ISupplier
{
  ...
}
```

## Abstract Classes and Interfaces
When we create an abstract class, we are creating a base class that might have one ore more **completed** methods but at least one or more methods are left uncompleted and declared `abstract`. If all the methods of an abstract class are uncompleted, then it is same as an interface.

When we create an interface, we are creating a set of methods without any implementation that must be overridden by the implemented classes.

The main differences between abstract class and interface is that a class can implement more than one interface but can only inherit from one abstract class.

## Aggregation
Aggregation is a special form of association, and means that one thing is made up (in part) of another thing.

## Lessons
 - Whenever we find common behavior in two or more places, look to abstract that behavior into a class, and then reuse that behavior in the common classes.
 - We should always favor **coding to the interface, not the implementation**.
 - The easiest way to make our software resilient to change is to make sure **each class has only one reason to change**.
   - When a class has more than one reason to change, it is probably **doing too many things**. Kindly try to break up the functionality into **multiple classes**, where **each individual class does only one thing** -- and therefore has only **one** reason to change.
 
## References
 - [Abstract Class versus Interface](https://www.codeproject.com/Articles/11155/Abstract-Class-versus-Interface)
