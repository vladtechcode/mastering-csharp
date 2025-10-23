## Using Variations of the Main() Method

```c#
// int return type, array of strings as the parameter.
static int Main(string[] args)
{
    // Must return a value before exiting!
    return 0;
}
```

```c#
// No return type, no parameters.
static void Main(){}
```

```c#
// int return type, no parameters.
static int Main(){
    // Must return a value before exiting!
    return 0;
}
```

```c#
static Task Main()
static Task<int> Main()
static Task Main(string[])
static Task<int> Main(string[])
```

## The Four Signatures Explained

1.  **`static Task Main()`**
    
    - **What it is:** An asynchronous entry point that does not return a value and does not accept command-line arguments.
    - **When to use it:** Perfect for simple asynchronous console apps where you don't need to pass in any parameters from the command line or signal an error with an exit code.
2.  **`static Task<int> Main()`**
    
    - **What it is:** An asynchronous entry point that returns an integer exit code but does not accept command-line arguments.
    - **When to use it:** Useful when your app needs to signal success (`return 0;`) or failure (`return 1;`) to the operating system or to scripts that called it, but doesn't need any command-line input.
3.  **`static Task Main(string[] args)`**
    
    - **What it is:** An asynchronous entry point that accepts command-line arguments but does not return an exit code.
    - **When to use it:** Ideal for asynchronous tools that need to be configured at launch (e.g., passing a filename or a URL) but where you don't need to return a specific success or failure code.
4.  **`static Task<int> Main(string[] args)`**
    
    - **What it is:** An asynchronous entry point that both accepts command-line arguments and returns an integer exit code.
    - **When to use it:** This is the most flexible signature. It's for complex asynchronous console applications that need to be configured by command-line arguments and also need to report a detailed success or failure status back to the caller.