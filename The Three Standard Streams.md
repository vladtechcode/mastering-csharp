## The Three Standard Streams

**Standard Input (stdin)** This is where the program reads user input from. By default, it's connected to the keyboard. When you call `Console.ReadLine()` or `Console.Read()`, you're reading from stdin.

**Standard Output (stdout)** This is where normal program output goes. By default, it's connected to the console window. When you call `Console.WriteLine()` or `Console.Write()`, you're writing to stdout.

**Standard Error (stderr)** This is a separate stream specifically for error messages and diagnostics. It's also connected to the console by default, but being separate allows errors to be handled differently from normal output.

## Why Have Separate Streams?

The separation of stdout and stderr is useful because:

- You can redirect normal output to a file while still seeing errors on screen
- Error messages won't get mixed up with regular data output
- You can process or log errors separately from normal program output

## Accessing the Streams

```csharp
// These properties give you direct access to the streams
TextReader input = Console.In;      // stdin
TextWriter output = Console.Out;    // stdout
TextWriter error = Console.Error;   // stderr

// Writing to different streams
Console.Out.WriteLine("Normal output");
Console.Error.WriteLine("Error message");
```

## Stream Redirection

Redirection means changing where these streams read from or write to. Instead of keyboard/console, you can connect them to files or other sources.

### Redirecting Output to a File

```csharp
using System;
using System.IO;

// Save the original output stream
TextWriter originalOut = Console.Out;

// Redirect stdout to a file
using (StreamWriter fileWriter = new StreamWriter("output.txt"))
{
    Console.SetOut(fileWriter);
    
    Console.WriteLine("This goes to the file");
    Console.WriteLine("Not visible in the console!");
    
} // File is closed here

// Restore original output
Console.SetOut(originalOut);
Console.WriteLine("Back to console output");
```

### Redirecting Input from a File

```csharp
// Save original input
TextReader originalIn = Console.In;

// Redirect stdin to read from a file
using (StreamReader fileReader = new StreamReader("input.txt"))
{
    Console.SetIn(fileReader);
    
    // Now ReadLine() reads from the file instead of keyboard
    string line = Console.ReadLine();
    Console.WriteLine($"Read from file: {line}");
}

// Restore original input
Console.SetIn(originalIn);
```

### Redirecting Error Stream

```csharp
using (StreamWriter errorLog = new StreamWriter("errors.log"))
{
    Console.SetError(errorLog);
    
    Console.Error.WriteLine("This error goes to the log file");
    Console.WriteLine("But this normal output still goes to console");
}
```

## Practical Example: Separating Output and Errors

```csharp
// Normal output and errors go to different places
using (StreamWriter outputFile = new StreamWriter("data.txt"))
using (StreamWriter errorFile = new StreamWriter("errors.txt"))
{
    Console.SetOut(outputFile);
    Console.SetError(errorFile);
    
    for (int i = 0; i < 5; i++)
    {
        if (i == 3)
        {
            Console.Error.WriteLine($"Error at iteration {i}");
        }
        else
        {
            Console.WriteLine($"Processing item {i}");
        }
    }
}
// data.txt will contain the normal messages
// errors.txt will contain only the error message
```

## Command-Line Redirection

You can also redirect streams from the command line when running your program:

```bash
# Redirect stdout to a file
myprogram.exe > output.txt

# Redirect stderr to a file
myprogram.exe 2> errors.txt

# Redirect both to different files
myprogram.exe > output.txt 2> errors.txt

# Redirect stdin from a file
myprogram.exe < input.txt

# Chain programs together (pipe)
program1.exe | program2.exe
```

## Real-World Use Cases

**Logging**: Redirect stderr to a log file while keeping stdout on the console for user feedback.

**Batch Processing**: Read input from a file instead of requiring manual keyboard entry.

**Data Pipeline**: One program's output becomes another program's input using pipes.

**Testing**: Redirect streams to capture output for automated testing instead of displaying to console.

**Background Services**: Services often redirect all output to log files since there's no console to display to.

## Complete Example: Log System

```csharp
public class LoggingExample
{
    public static void Main()
    {
        // Set up logging
        TextWriter originalOut = Console.Out;
        TextWriter originalError = Console.Error;
        
        using (StreamWriter logFile = new StreamWriter("app.log", append: true))
        {
            // Create a multi-writer that writes to both console and file
            MultiTextWriter multiWriter = new MultiTextWriter(originalOut, logFile);
            Console.SetOut(multiWriter);
            Console.SetError(multiWriter);
            
            Console.WriteLine($"[{DateTime.Now}] Application started");
            
            try
            {
                ProcessData();
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"[{DateTime.Now}] ERROR: {ex.Message}");
            }
            
            Console.WriteLine($"[{DateTime.Now}] Application ended");
        }
    }
    
    static void ProcessData()
    {
        // Your application logic here
        Console.WriteLine("Processing data...");
    }
}

// Helper class to write to multiple streams
class MultiTextWriter : TextWriter
{
    private TextWriter[] writers;
    
    public MultiTextWriter(params TextWriter[] writers)
    {
        this.writers = writers;
    }
    
    public override void Write(char value)
    {
        foreach (var writer in writers)
            writer.Write(value);
    }
    
    public override System.Text.Encoding Encoding => System.Text.Encoding.UTF8;
}
```

Stream handling gives you powerful control over where your program's input comes from and where its output goes, making your applications more flexible and suitable for different environments.