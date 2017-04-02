# Requirement Analysis

What is a Requirement?
A requirement is a **specific thing** the **system** has to do to **work correctly**.

A requirement is a **singular need** detailing what a particular product or service should **be** or **do**. We can **test** that thing to make sure you've actually fulfilled the requirement.

Remember, the **users** decide when a system works correctly. So if developers leave out a requirement, or even if the users forget to mention something to developers, the system is **not working correctly**.

## Gathering Requirements
When it comes to requirements, the best thing developers can do is **let the users talk**. Developers need to pay attention to what the system needs to do and developers can thus figure out how the system will do those things later.

## Writing Use Cases
A use case describes **what** the system **does** to accomplish a **particular goal of the users**.

A use case focuses on a **single** goal. Use cases are **detail-oriented**; **Use Case Diagrams** are focused more on the big picture.

An **Actor** in the use case diagram is anything that interacts with our system, but isn't part of the system.

Use cases are all about "**what**". Developers should **not worry about the "how"** when writing use cases.

A use case is a technique for capturing the potential requirements  of a new system or software change. Each use case provides one or more **scenarios** that convey how the system should **interact** with the end user or another system to achieve a **specific goal**.

There are 3 basic parts to a good use case.
 1. **Clear Value**: Every use case must have a clear value to the system by helping the users achieve their goal.
 2. **External Initiator**: Every use case is started off by an external initiator which is outside of the system, such as the user.
 3. **Start and Stop**: Every use case must have a definite **starting** and **stopping point**.

## Analysis
Our software has to **work in the real world**, not just in a perfect world. We have to think about our software in a different context where things go wrong a lot more often. **Analysis** helps us to ensure our system works in a **real-world context**. Analysis helps us figuring out potential problems before the software is released out into the real world.

## Class Diagrams
Class diagrams are a great way to get an overview of the system, and show the parts of the system to other developers. However, there are things they don't show.
 - Details of how the method should work;
 - Reasons of having the parameter(s) in the method;
 - General idea behind the class.
 
## Solving Big Problems
 - Listen to the users, and figure out what they want us to build;
 - Put together a **Feature List**, in language the users understand;
 - Make sure our features are what the users actually want;
 - Create blueprints of the system using **Use Case Diagrams** (and use cases);
 - Break the big system up into lots of smaller section;
 - Apply **Design Patterns** to the smaller section of the system;
 - Use basic **OOAD Principles** to design and code each smaller section.

## Lessons
 - Having a task list can help showing the top management exactly what developers are working on, and what work developers think is left to finish the project.
 - Sometimes even the users do not know what they really want.
   - It's developers' job to ask the users questions to find out what they want before deciding what the system shoud do.
   - Developers need to think beyond what users asked for and anticipate their needs.
   - A good set of requirements goes beyond just what the users tell the developers. Developers need to make sure that the system works, even in unusual or unexpected circumstances.
 - Additional requirements almost always come up as developers work on a project.
 - Write the use cases in a way that makes sense to developers, managers, and users.
 - Analysis and use cases let us show other developers, managers, and users how our system works in a **real world context**.
 - With a good use case complete, **textual analysis** is a quick and easy way to figure out the classes in our system.
