# Runtime Code Inspecting

When the running code hits a breakpoint and suspends, we can inspect the variables and call stacks to determine what is going on. To do so, just mouse-hover over a variable to see the value(s) and reference(s) it currently contains.

## DataTip
The most commonly used way to look at variables is the **DataTip**. When we are in debugging mode, we can mouse-hover the variable and then the DataTip will appear showing the value of that variable. If the variable is an object, we can further expand the object by clicking on the arrow to see the elements of that object.

![DataTip](http://www.codeproject.com/KB/cs/MasteringInDebugging/debug20.png)

Data tips are always evaluated in the context where execution is suspended, and **not where the cursor is hovering**. If we mouse-hover over a variable in another function with the same name as a variable that is in the current context, the value of the variable in the other function is displayed as the value of the variable in the current context.

When we click on that pin icon that it will pin the DataTip for that variable like following. 

![Pin DataTip](http://2.bp.blogspot.com/-rtprzCDgyT4/UWODvpTdhhI/AAAAAAAAExE/IjIKNXMqf8Q/s320/PinDataTip.png)

A pinned DataTip can be unpinned but unpinning a DataTip turns it into a floating DataTip with a orange color.

![Unpinned DataTip](http://2.bp.blogspot.com/-MvBhNZ-o8rA/UWOCslMHZ4I/AAAAAAAAEw8/0M72aswJzB0/s320/FloatingDataTip.png)

To remove a pinned DataTip, we can choose "Close" instead of "Unpin". To remove all pinned DataTips, we simply need to go **Debug > Clear All DataTips**.

We can also add comments with the DataTips.

![Comment in DataTip](http://2.bp.blogspot.com/-2SEArJAlPtM/UWOgBw49DDI/AAAAAAAAExk/YEEfjRKVrmc/s320/CommentsWithDataTips.png)

The data tips can also be exported. These exported data tips can be imported back into another debuggin session even on other machines with the options of **Export DataTips** and **Import DataTips** in Debug menu. This is specially useful to share the data tips across the team (**other team members need to have the same folder structure for the code**).

## Autos: See variables used near the Instruction Pointer
Besides having developer to mouse-hover the variable to inspect the value of a variable, the **Autos Window** (**Debug > Windows > Autos**) will automatically populate with all the variables used in the current statement (the line where the yellow Instruction Pointer is) and some surrounding statements. The scope of what variables automatically populate from the surrounding statements depends on the language of the code.

![Autos Window](https://msdnshared.blob.core.windows.net/media/2016/07/image_thumb386.png)

## Locals: See variables that exist in the local scope of the current Stack Frame
The **Locals Window** (**Debug > Windows > Locals**) will populate with the local variables in current scope. Like the Autos Window, variables that appear here are automatically populated. Thus, the Autos Window is a subset of the Locals Window.

In all of our variable windows, when any values of the variables change the new values will appear in red text.

![Locals Window](https://msdnshared.blob.core.windows.net/media/2016/07/image_thumb387.png)

## Watch and Quick Watch
We can use the **Watch Windows** (**Debug > Windows > Watch > Watch (1, 2, 3, 4)**) and **QuickWatch Window** (**right-click on variable > Debug > QuickWatch**) to watch variables and expressions during a debugging session. The difference is that the Watch Window can display several variables, while the QuickWatch Window displays a single variable at a time.

We can also add any valid expression recognized by the debugger.

![Observing expressions with the Watch Window](https://i-msdn.sec.s-msft.com/dynimg/IC848480.jpeg)

In certain circumstances there will be a refresh icon when an expression is evaluated in the Watch Window. We can generally refresh the value by clicking on the icon, but in some cases we first need to know why the value was not evaluated. We can know the reasons by mouse-hovering the refresh icon to get a tooltip providing information about why the expression was not evaluated.
 
### Side Effects
Evaluating some expressions can change the value of a variable or otherwise affect the state of the program. For example, evaluating the following expression changes the value of `var1`:

```
var1 = var2
```

This is known as **Side Effect**. Side Effects can make debugging more difficult by changing the way the program operates.

An expression that is known to have Side Effects is evaluated only once, i.e. when we first enter it. Subsequent evaluations are disabled.

One way to avoid all side effects is to turn off automatic function evaluation (**Tools > Options > Debugging > Enable property evaluation and other implicit function calls**).

## Immediate: The scratch pad
While stopped at a line of code, we can type a variable or expression into the **Immediate Window** (**Debug > Windows > Immediate**) and hit enter to view the result. The Immediate Window evaluates expressions just like the Watch Windows and can result in **Side Effects**.

We can also use the Immediate Window to execute complex expressions (even evaluate **Lambda Expressions**) and view the results without having to edit and re-execute our code.

![Immediate Window](https://msdnshared.blob.core.windows.net/media/2016/07/image_thumb390.png)

Immediate Window also can execute a function or subroutine while the application is not running. If the function or subroutine contains a breakpoint, the debugger will break execution at the appropriate point. We can then use the debugger windows to examine the program state. This feature is called **Debugging at Design Time**.

## References
 - [7 Ways to Look at the Values of Variables While Debugging in Visual Studio](https://blogs.msdn.microsoft.com/visualstudioalm/2016/07/15/7-ways-to-look-at-the-values-of-variables-while-debugging-in-visual-studio/)
 - [Tips & Tricks : Visual Studio - Debugging Using Data Tips](http://www.shujaat.net/2013/04/tips-tricks-visual-studio-debugging.html)
 - [Did you know… What’s the difference between the Autos window and the Locals window? – #316](https://blogs.msdn.microsoft.com/saraford/2008/09/18/did-you-know-whats-the-difference-between-the-autos-window-and-the-locals-window-316/)
 - [Walkthrough: Debugging at Design Time](https://msdn.microsoft.com/en-us/library/83hd8f1e.aspx)
 - [Watch and QuickWatch Windows](https://msdn.microsoft.com/en-us/library/0taedcee.aspx)
