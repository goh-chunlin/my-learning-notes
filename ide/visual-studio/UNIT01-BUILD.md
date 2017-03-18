# Build

## Debug and Release
There are two basic types of build configuration: **Debug** and **Release**.

**Debug** produces a slower, larger executable which allows for a richer interactive run-time debugging experience. **It should never be shipped in the production environment.**

**Release** produces a faster, more optimized executable which is appropriate to ship.

We can also specify Build Platform to target, such as **x86** (32bit Intel CPUs), **x64** (64bit Intel CPUs), and **ARM** (ARM CPUs). Take note that ARM is a family of CPUs based on RISC architecture developed by **Advanced RISC Machines**. This option is only supported for certain app types, for example Universal Windows Platform (UWP). When deploy UWP apps to Raspberry Pi 2, which is running on ARM CPU, we need to specify the Build Platform to be ARM.

There is one more Build Platform option which is called **AnyCPU**. AnyCPU means that the .NET framework will figure out, based on OS bitness, whether to run the program in 32-bit or 64-bit. In Visual Studio 2015, AnyCPU is the default with the new sub-type known as **"AnyCPU 32-bit Preferred"**. This makes the difference between AnyCPU and x86 to be only this: a .NET application compiled to x86 will fail to run on an ARM Windows system, but an “Any CPU 32-bit preferred” application will run successfully. The option of **"Prefer 32-bit"** is only available for executable type of projects. For all other project types, such as ASP .NET projects, the option should be grayed out.

When the project is built, the configuration and platform values are also used to determine what project directory path is created to store the executable in the following format: `<path-to-project>\<project-name>\<configuration>\<platform>`. So, a project with a configuration of Debug and a platform of x86 would be found under `Projects\MyProjectNameHere\MyProjectNameHere\bin\Debug\x86`.

## References
 - [Getting Started with Debugging in Visual Studio 2015](https://msdn.microsoft.com/en-us/library/dn986851.aspx)
 - [What does the Visual Studio "Any CPU" target mean?](http://stackoverflow.com/questions/516730/what-does-the-visual-studio-any-cpu-target-mean)
 - [What AnyCPU Really Means As Of .NET 4.5 and Visual Studio 11](http://blogs.microsoft.co.il/sasha/2012/04/04/what-anycpu-really-means-as-of-net-45-and-visual-studio-11/)
