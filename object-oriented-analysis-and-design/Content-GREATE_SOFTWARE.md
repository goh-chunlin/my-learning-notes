# Building Greate Software

## What is Great Software?
 - Great software always does what the customer wants it to. If customers think of alternative ways to use the software, it should not break or even generate unexpected results;
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
 
## Objects are Not Xaxiubao
 - Each object is interested in doing its job, and only its job, to the best of its ability.
 - There is nothing a well-designed objec hates more than being used to do something that really isn't its true purpose.
 
## Lessons
 - Don't create problems to solve problems.
 - Ditching string comparisons.
 - Code that is not fragile is generally referred to as **robust** code**.
 - Trying to do too much design before we have at least get the basic functionality down can end up being a waste. This is because a lot of the design will change as we are adding new pieces of functionality to our classes and methods.
 - Use a textual description of the problem we are trying to solve to make sure that **our design lines up with the intended functionality** of our app.
