# Breakpoints

## Simple Breakpoints
A breakpoint indicates where Visual Studio should suspend the running code so that developer can take a look at the values of variables, or the behavior of memory, or whether or not a branch of code is getting run.

There is no need to rebuild a project after setting and removing breakpoints.

To set a breakpoint, just click in the far margin of the line where the break needs to occur.
![Setting breakpoint](https://i-msdn.sec.s-msft.com/dynimg/IC796018.jpeg)

When the code breaks, the marked line of code has not executed yet. At this point, we may need to do some code navigation with debugger such as executing the instructions for the line of code marked by the breakpoint and inspect the changed values.

To delete all breakpoints, simply use the **Ctrl + Shift + F9** keyboard shortchut.

## Code Navigation with Debugger
When we start a debugging session using F5, the program will be started with the **Debugger** attached. When we debug, the yellow line indicated the code that will be executed next.

![Yellow Line in Visual Studio](https://i-msdn.sec.s-msft.com/dynimg/IC860476.jpeg)

### F11: Step into Code, Line by Line
To stop on **each statement** while debugging, use the **F11** keyboard shortcut.

On a nested function call, **Step Into** steps into the most deeply nested function. If you use Step Into on a call like `Func1(Func2())`, the debugger steps into the function `Func2` first.

As you execute each line of code, you can hover over variables to see their values, or use the Locals and Watch windows to watch their values change.

When you are in a function, we can use the **Shift + F11** keyboard shortcut to perform **Step Out** so that the debuger continues running code and suspends execution when the current function returns.

### F10: Step over Code, Skipping Functions
Often we don't need to see what happens in a particular function so we can use the **F10** keyboard shortcut to make the debugger skip through the function (the function will still be executed). So when **Step Over** is used, if the current line contains a function call, Step Over runs the code then suspends execution at the first line of the code after the called function returns.

### Run to Cursor, Setting a Temporary Breakpoint
Instead of keep setting up breakpoints and removing them afterwards, we can also place our cursor on an executable line of code in a source window, right-click on it, and then choose **Run to Cursor** to setup temporary breakpoint.

### Run to Function, Setting Function Breakpoint
We also can tell the debugger to run the application until it reaches a specified function which is specified by name or is chosen from the call stack.

To specify a function by name, choose **Debug > New Breakpoint > Break at Function**, then enter the name of the function and other identifying information. To narrow the function specification:
 - Use the fully qualified function name, eg. Namespace1.ClassX.MethodA();
 - Add the parameter types of an overloaded function, eg. MethodA(int, string);
 - Use the '!' symbol to specify the module, eg. Namespace1.dll!MethodA.
 
### Move Instruction Pointer
![Instruction Pointer](https://i-msdn.sec.s-msft.com/dynimg/IC577264.jpeg)

When the debugger is paused, the instruction pointer can be moved **either forward or backward** to set the next statement of code to be executed by dragging the yellow arrow to a location where we want to set the next statement in the same source file.

Things to note when moving the Instruction Pointer.
 - To set the next statement, the debugger must be in break mode.
 - Instructions between the old and new execution points are not executed.
 - If the execution point is moved backwards, intervening instructions are **not undone**.
 - Moving the next statement to another function or scope usually results in call-stack corruption, causing a run-time error or exception. The debugger normally will prompt a dialog box with a warning to allow developer to cancel the operation.

## Conditional Breakpoints
If we want our code is suspended **only** when specific conditions are met, for example when we are in a loop or recursion, we can use a conditional breakpoint. 

To set a conditional breakpoint and suspend the code when a variable is set to a certain value or passes a certain threshold, click in the margin to set a breakpoint, and then select the **Settings* (the option with Cog icon) from the hover menu that appears.

![Cog](https://i-msdn.sec.s-msft.com/dynimg/IC796019.jpeg)

A peak window of **Breakpoint Settings** will appear without blocking the code. The Breakpoint Settings offer additional conditions and actions that developer can perform in the breakpoint that can potentially improve the debugging productivity.

![Breakpoint Settings in a Peak Windown](https://i-msdn.sec.s-msft.com/dynimg/IC796020.jpeg)

### Conditions
The **Conditions** available are **Conditional Expression**, **Hit Count**, and **Filter**.

For Conditional Expression, the condition can be any valid expression that is recognized by the debugger. Choose **Is true** if we want to break when the expression is satisfied, or choose **When changed** if we want to break when the value of the expression has changed.

Hit Count tells the debugger to break after the breakpoint has been hit by a certain number of times. The count is zero based.

Filter breakpoint will let debugger to break based on the machine process or thread information. This is useful when we are debugging a shared code running parallel in different processes, threads, and machines.

### Actions
**Actions**, at this point, is only to log a message to the **Output Window**. So instead of stopping and inspecting codes manually under the debugger every single time, we can just print the logs out for later review.

The message allows us to include the value of a variable or other expression by placing it in curly braces, such as "The value of x is {x}". If we want to insert curly brace and backslash, we just need to escape it using another backslash.

In addition, the following keywords can be accessed in the message using "$".
 - $ADDRESS: Address of the current instruction
 - $CALLER: Name of the function calling the current function
 - $CALLSTACK: Current call stack
 - $FUNCTION: Current function name
 - $PID: Current process id
 - $PNAME: Current process name
 - $TID: Current thread id
 - $TNAME: Current thread name

## Just My Code
There is a setting called **Just My Code** in the debugger (not supported for device projects). When Just My Code is disabled, the debugger can step into non-user code and non-user code appears in the debugger windows. To turn it off, simply go to **Tools > Options > Debugging** and untick the **Enable Just My Code** checkbox.

To distinguish user code from non-user code, Just My Code looks at symbol (.pdb) files and program optimizations. The debugger considers code to be non-user code when the binary is optimized or when the .pdb file is not available.

## References
 - [Navigating through Code with the Debugger](https://msdn.microsoft.com/en-us/library/y740d9d3.aspx)
 - [Breakpoint Configuration Experience](https://channel9.msdn.com/events/visual-studio/connect-event-2014/711)
 - [Just My Code](https://msdn.microsoft.com/en-us/library/dn457346.aspx)
