# Design Principles

A design principle is a basic tool or technique that can be applied ti designing or writing code to make that code more maintainable, flexible, or extensible.

## Open-Closed Principle (OCP)

> Classes should be open for extension, and closed for modification.
>
> -- Open-Closed Principle

OCP is about **allowing change**, but doing it **without requiring developers to modify existing code**.

We **close** classes by not allowing anyone to touch the working code in those classes but we **open** classes by allowing them to be subclassed and extended.

Extending another class is **not the only way** to use OCP. As long as our code is closed for modification but open for extension, we are using the OCP. For example, if we have serveral private methods in a class, those are closed for modification. Then we have several public methods that invoke those private methods in different ways. The behavior of the private methods are thus extended without having their code changed.

OCP is a combination of **encapsulation** and **abstraction**. We find the behavior that stays the same, and abstracting that behavior away into a base class, and then locking that code up from modification. When we need to update the behavior, our subclasses handle the changes by entending the base class.

**Change is the great constant in software development.** With the OCP, we allow for change through extension, rather than having to go back and modify our existing codes. Hence, the originally working codes **won't be messed around** with.

## Don't Repeat Yourself (DRY)

> Avoid duplicated codes by abstracting out things that are in common and placing those things in a single location.
>
> -- Don't Repeat Yourself Principle

Abstracting out duplocated code is a good start to using DRY. When we avoid duplicated codes, we also make sure that we **only implement each feature and requirement in our application one single time**.

DRY is about having a **single source** for a particular piece of information or behavior. However that single source has to **make sense**. Rather than just tossing code that appears more than once into a single class, we neeed to make sure each piece of information and behavior in the system has **a single, clear place where it exists**. That way, our system always knows exactly where to go when it needs that information or behavior.

DRY is about a lot **more than just code**. For example, a requirement should be implemented one time and use cases shouldn't have overlap.

So DRY is not just removing duplication, it's also about **making good decisions** about how to break up the system functionality.

## Single Responsibility Principle (SRP)

> Every object in the system should have a single responsibility, and all the object's services should be focused on carrying out that single responsibility.
>
> -- Single Responsibility Principle

SRP is all about **responsibility**, and **which objects** in the system do that.

We have implemented SRP correctly when each of our objects has **only one reason to change**.

In good apps, one class does one thing and does it well, and no other classes share that behavior.

**Cohesion** is actually just another name for the SRP. If we are writing **highly cohesive** software, we are already correctly applying the SRP.

## Liskov Substitution Principle (LSP)

> Subtypes must be substitutable for their base types.
>
> -- Liskov Substitution Principle

LSP is all about **well-designed inheritance**.

When we inherit from a base class, we must be able to substitute our subclass for that base class without things going terribly wrong.

When we use inheritance, our subclasses get all the methods from their superclass, even if we don't want those methods. Hence, if we have used inheritance badly, then we are going to end up with a lot of methods that we don't want because they probably also don't make any sense on the subclasses.
  - So we need to make sure our subclasses can substitude for their base types, which is just following the LSP.

LSP is **not about subclassing**; it's about **when to subclass**. If our subclass really is substitutable for its base type, then we have probably following LSP. Otherwise, then we might look at other object-oriented solutions like **composition**, **aggregation** or **delegation**.
  
## Delegate Principle

> Delegation is when we hand over the responsibility for a particular task to another class or method.
> 
> -- Delegate Principle

Delegation is also one of several alternatives to inheritance.

Delegation is best used when we want to **use another class's functionality**, as is, **without changing that behavior at all**.

## Lessons
 - Among delegated class, delegating class, aggregated class, and composite class, a subclass is the only class that **change** another class's behavior.
