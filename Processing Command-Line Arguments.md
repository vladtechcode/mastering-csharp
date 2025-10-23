## Processing Command-Line Arguments

```C#
static int Main(string[] args)
{
	foreach(string arg in args)
	{
		Console.WriteLine("Arg: {0}", arg);
	}
		Console.ReadLine();
	return 0;
}
```

Finally, you are also able to access command-line arguments using the static `GetCommandLineArgs()` method of the `System.Environment` type. The return value of this method is an array of strings. The first entry holds the name of the application itself, while the remaining elements in the array contain the individual command-line arguments.

```c#
// Get arguments using System.Environment.
string[] theArgs = Environment.GetCommandLineArgs();
foreach(string arg in theArgs)
{
	Console.WriteLine("Arg: {0}", arg);
}
	Console.ReadLine();
return 0;
```
 