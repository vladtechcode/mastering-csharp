The `System.Console` class in C# provides functionality for reading from and writing to the console (command-line interface). It's a static class that handles standard input, output, and error streams.

## Key Features

**Input and Output** The class allows you to read user input from the keyboard and write text output to the console window. This is essential for creating command-line applications and debugging.

**Stream Handling** Console works with three standard streams: standard input (stdin), standard output (stdout), and standard error (stderr). You can redirect these streams if needed.

**Formatting and Colors** You can control text appearance with colors, cursor positioning, and formatting options to create more interactive console applications.

## Common Output Methods

- `Write()` - Writes text without a newline
- `WriteLine()` - Writes text followed by a newline
- `Clear()` - Clears the console screen
- `Beep()` - Plays a beep sound through the console speaker

## Common Input Methods

- `Read()` - Reads the next character from input stream
- `ReadLine()` - Reads a line of text (until Enter is pressed)
- `ReadKey()` - Reads a single key press, optionally without displaying it

## Formatting and Appearance

- `ForegroundColor` - Gets or sets the text color
- `BackgroundColor` - Gets or sets the background color
- `ResetColor()` - Resets colors to default
- `CursorLeft` and `CursorTop` - Gets or sets cursor position
- `SetCursorPosition(int, int)` - Moves the cursor to specific coordinates
- `Title` - Gets or sets the console window title

## Window Properties

- `WindowWidth` and `WindowHeight` - Gets or sets console window dimensions
- `BufferWidth` and `BufferHeight` - Gets or sets the buffer area size
- `CursorVisible` - Shows or hides the cursor

## Example Usage

```csharp
// Basic output
Console.WriteLine("Hello, World!");
Console.Write("Enter your name: ");

// Reading input
string name = Console.ReadLine();
Console.WriteLine($"Hello, {name}!");

// Reading a key press
Console.WriteLine("Press any key to continue...");
ConsoleKeyInfo key = Console.ReadKey(true); // true = don't display the key
Console.WriteLine($"You pressed: {key.Key}");

// Using colors
Console.ForegroundColor = ConsoleColor.Green;
Console.WriteLine("This text is green!");
Console.BackgroundColor = ConsoleColor.Blue;
Console.WriteLine("Green text on blue background");
Console.ResetColor();

// Formatting with placeholders
int age = 25;
Console.WriteLine("Name: {0}, Age: {1}", name, age);

// String interpolation (modern approach)
Console.WriteLine($"Name: {name}, Age: {age}");

// Cursor positioning
Console.SetCursorPosition(10, 5);
Console.WriteLine("Text at position (10, 5)");

// Clear screen and set title
Console.Clear();
Console.Title = "My Console App";

// Reading without echo (useful for passwords)
Console.Write("Enter password: ");
string password = "";
while (true)
{
    var keyInfo = Console.ReadKey(true);
    if (keyInfo.Key == ConsoleKey.Enter) break;
    password += keyInfo.KeyChar;
    Console.Write("*");
}
Console.WriteLine();

// Error output
Console.Error.WriteLine("This is an error message");
```

## Advanced Features

**Reading specific input types:**

```csharp
// Reading numbers safely
Console.Write("Enter a number: ");
if (int.TryParse(Console.ReadLine(), out int number))
{
    Console.WriteLine($"You entered: {number}");
}
else
{
    Console.WriteLine("Invalid number");
}
```

**Stream redirection:**

```csharp
// Redirect output to a file
using (StreamWriter writer = new StreamWriter("output.txt"))
{
    Console.SetOut(writer);
    Console.WriteLine("This goes to the file");
}
```

**Handling special keys:**

```csharp
ConsoleKeyInfo keyInfo = Console.ReadKey();
if (keyInfo.Key == ConsoleKey.Escape)
{
    Console.WriteLine("\nEscape pressed!");
}
if (keyInfo.Modifiers == ConsoleModifiers.Control)
{
    Console.WriteLine("\nControl key was held down!");
}
```

The Console class is fundamental for creating command-line tools, debugging applications, and building text-based user interfaces in C#.