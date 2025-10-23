There are some rules around using top-level statements:
- Only one file in the application can use top-level statements.
- When using top-level statements, the program cannot have a declared entry point.
- The top-level statements cannot be enclosed in a namespace.
- Top-level statements still access a string array of args.
- Top-level statements return an application code (see the next section) by using a return.
- Functions that would have been declared in the Program class become local functions for the top-level statements.
- The top-level statements compile to a class named Program, allowing for the addition of a partial Program class to hold regular methods.
- Additional types can be declared after all top-level statements. Any types declared before the end of the top-level statements will result in a compilation error.