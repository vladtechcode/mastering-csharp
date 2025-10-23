## How to create a solution and a console project

```c#
dotnet new sln -n Chapter3_AllProjects
dotnet new console -lang c# -n SimpleCSharpApp -o .\SimpleCSharpApp -f net6.0
dotnet sln .\Chapter3_AllProjects.sln add .\SimpleCSharpApp
```
## Breaking Down a Simple C# Program

Prior to `C# 10`, you were required to write the following:

```c#
using System;

namespace SimpleCSharpApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

The `Console`class is contained in the `System` namespace, and with the implicit global namespaces provided by `.NET 6/C# 10`, the `using System;` statement is no longer needed. Both the `namespace` and the `Program` class can be removed due to the [Top-level statements](../CSharp/Top-level%20statements.md) functionality introduced in `C# 9`.

It is possible for a single executable application to have more than one application object (which can be useful when performing unit tests), but then the compiler must know which `Main()` method should be used as the entry point. This can be done via the element in the project file or via the `<Startup Object>` drop-down list box, located on the Application tab of the Visual Studio project properties window.
