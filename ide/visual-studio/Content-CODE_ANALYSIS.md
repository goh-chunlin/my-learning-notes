# Code Analysis

## Static Code Analysis
**Static Code Analysis** is a fancy way of saying "automatically check my code for common problems that can lead to run-time errors or problems in code management". Static Code Analysis helps us to keep our code maintainable and to learn code style techniques.

## Setup
You can enable Code Analysis to automatically run before each build of a managed code project. To enable it, please follow the steps below.
 1. In **Solution Explorer**, right-click the project, and then click **Properties**.
 2. In the properties dialog box for the project, click **Code Analysis**.
 3. Specify the build type in **Configuration** drop-down and the target platform in **Platform** drop-down.
 4. Tick the checkbox **Enable Code Analysis on Build**.
 
If there are errors and warnings found after running the Code Analysis, they will be listed in Error List Window.

## Code Matrics
Code metrics is a set of software measures that provide developers better insight into the code they are developing. By taking advantage of code metrics, developers can understand which types and/or methods should be reworked or more thoroughly tested.

To generate code metrics results for a project, please follow the steps below.
 1. In **Solution Explorer**, select the project.
 2. Right-click your selections and then click **CalculateCode Metrics**.
 3. The results are generated and displayed in the **Code Metrics Results Window**.
 
The following list shows the code metrics results that Visual Studio calculates.

### Maintainability Index
It calculates an index value between 0 and 100 that represents the relative ease of maintaining the code. A high value means better maintainability.

### Cyclomatic Complexity
It masures the structural complexity of the code. A program that has complex control flow will require more tests to achieve good code coverage and will be less maintainable.

### Depth of Inheritance
It indicates the number of class definitions that extend to the root of the class hierarchy. The deeper the hierarchy the more difficult it might be to understand where particular methods and fields are defined or/and redefined.

### Class Coupling
It measures the coupling to unique classes. High coupling indicates a design that is difficult to reuse and maintain because of its many interdependencies on other types.

### Lines of Code
It indicates the approximate number of lines in the code because the count is based on the Intermediate Language code. A very high count might indicate that a type or method is trying to do too much work and should be split up. It might also indicate that the type or method might be hard to maintain.

## References
 - [How to: Enable and Disable Automatic Code Analysis for Managed Code](https://msdn.microsoft.com/en-us/library/dd547175.aspx)
 - [Code Metrics Values](https://msdn.microsoft.com/en-us/library/bb385914.aspx)
 - [How to: Generate Code Metrics Data](https://msdn.microsoft.com/en-us/library/bb385908.aspx)
