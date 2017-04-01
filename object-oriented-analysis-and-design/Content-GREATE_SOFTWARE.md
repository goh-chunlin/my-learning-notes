# Building Greate Software
**Object-Oriented Analysis and Design (OOAD)** helps us write great software. It is an approach to writing software that focuses on making sure our code **does what is is supposed to, and that it is well designed**. The code will be flexible, easy to make changes to it and reusable.

## What is Great Software?
 - Great software always does what the customer wants it to. If customers think of alternative ways to use the software, it should not break or even generate unexpected results.
 - The software should be easy to maintain and easy to extend. The design of the software must be solid and flexible;
 - Objects in the software are loosely coupled, the code is open for extension but closed for modification.
 - No duplicate of code which helps the code to be more reusable without the developers to rework everything over and over again.
 
## Steps to Build Great Software
 1. Make sure **our software does what it is supposed to do** by **getting good requirements and doing analysis**;
 2. Apply basic **object oriented principles to add flexibility**;
 3. Strive for a **maintainable, reusable design** by **applying patterns and principles to make the software is ready to use for years to come**.
 
## Ditching String Comparisons
 - Get rid of all those annoying string comparisons. Please use **enums**.
 - Benefit of using enums is that methods or classes use them are protected from any values not defined in the enum. So we will achieve not only type safety but also value safety.
 
```
public enum DiscountType
{
 [EnumDescription("Dollar")]
 DOLLAR = 0,
 [EnumDescription("Percentage")]
 PERCENTAGE = 1
}
```

```
public static class EnumExtensions
{
 public class EnumDescription : Attribute
 {
  public string Text { get; private set; }
  
  public EnumDescription(string text)
  {
   Text = text;
  }
 }
 
 public static string ToDescription(this Enum enumeration)
 {
  var type = enumeration.GetType();
  var memberInfo = type.GetMember(enumeration.ToString());
  
  if (memInfo != null && memInfo.Length > 0)
  {
   var attrs = memInfo[0].GetCustomAttributes(typeof(EnumDescription), false);
   if (attrs != null && attrs.Length > 0)
   {
    return ((EnumDescription)attrs[0]).Text;
   }
  }
 }
}
```
 
## Objects are Not Xaxiubao (Loosely Coupled)
 - Objects should do what their names indicate. An object named Airplane should not do takeTicket().
 - Each object should represent a single concept. Avoid a Duck object that represents a real quacking duck and a yellow plastic duck.
 - Unused properties are a dead giveaway. If we rarely have values for a certain property, why is that property part of the object?
 - Object should be independent of each other, i.e. **loosely coupled**. Loosely coupled objects can be taken from one app and easily reused in another, because they're not tightly tied to other objects' code.
 - Loosely coupled apps are usually more flexible, and easy to change. A change made to one object's behavior will not affect all the rest of other objects in the system.
 - Find the parts of our application that change often, and try and separate them from the parts of our application that do not change.
 
## Lessons
 - Don't create problems to solve problems.
 - Ditching string comparisons.
 - Code that is not fragile is generally referred to as **robust** code.
   - It takes very little for something to go wrong with an application that is fragile.
 - Trying to do too much design, before we have at least get the basic functionality down, can end up being a waste.
   - This is because a lot of the design will change as we are adding new pieces of functionality to our classes and methods.
 - Use a textual description of the problem we are trying to solve to make sure that **our design lines up with the intended functionality** of our app.
 - **Each object is interested in doing its job, and only its job**, to the best of its ability. There is nothing a well-designed objec hates more than being used to do something that really isn't its true purpose.
 - **Encapsulation**: Break our app into logical parts, and then keep those parts separate. This is to make sure that we can change one part without having to change all the other parts in the system.
 - Any time we see **duplicated code**, look for a place to **encapsulate**!
 - **Delegate**: When an object needs to perform a certain task, and instead of doing the task directly, it asks another more relevant object to handle the task. Delegation should **make the code more reusable** by letting each object **worry about only its own functionality**.
