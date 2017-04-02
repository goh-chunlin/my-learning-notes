# Architecture

It is not enough to just figure out the individual pieces of a big problem. We also need to know a little bit about how those pieces fit together, and which ones might be more important than others; that way, we'll know what we should work on **first**.

Architecture is our **design structure**, and highlights the **most important** parts of our system, and the **relationship** between those parts.

Architecture is the organizational structure of a system, including its decomposition into parts, their connectivity, interaction mechanism, and the guiding principles and decisions that you use in the design of a system.

## Functionality Analysis
The first step is always to make sure a system does what it is supposed to do. In big projects, we have been using a **Feature List** to figure those things out. Now we need to figure out which functionalities are the **most important**.

So, architecture is not just about the relationships between parts of the system; it's also about figuring out which parts are the **most important**, so we can start building those parts first.

There are 3 questions we can ask to figure out if something is architecturally significant.
 1. Is the feature really **core** to what a system actually is?
    - Can we imagine the system without that feature? If not, then that feature is part of the essence of the system.
 2. What does the feature mean?
    - If we are not sure what the description of a particular feature **really means**, it's probably pretty important that we need to pay attention to that feature.
    - Spend time on those features early, rather than later.
 3. How do we implement the feature?
    - Another place to focus attention early on is on features that seem **really hard to implement**, or are **totally new** programming tasks for the developers.
    
## Risks
 - Focus on one feature at a time to reduce risk in the project.
 - Don't get distracted with features that won't help reduce risk.

## Lessons
 - The things in the system that are really important are **architecturally significant**, and we should focus on them **first**.
 - The **essence** of a system is what that system is at its most **basic level**.
 - Sometimes the best way to **write great code** is to **hold off** on writing code **as long as we can**.
 - Use **commonality analysis** to build software solutions that are flexible.
 - Users are a lot more interested in software that does what they want, and comes in on time, than they are in code that developers think is really cool.
