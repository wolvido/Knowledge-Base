---
keywords: |-
  how to error
  defensive programming
  exceptions
  how to exception
---
#cSharp 
### syntax:
```c#
try
{
    // Code that may cause an exception
}
catch (ExceptionType exceptionVariable) 
{
    // Code to handle the exception
    // NOTE: Code will continue if catch is executed, code will stop if no catch is detected for the exception
}
//you can also add another catch, optional.
finally // optional
{
	// Will run even if exception occurs or if exception is caught
}
```
- **ExceptionType**: This is the type of exception you want to catch. It can be a specific exception type (e.g., `DivideByZeroException`, `FileNotFoundException`) or a base exception type (e.g., `Exception`) that can catch any exception derived from it.
- **exceptionVariable**: This is the name of the variable that represents the caught exception. You can choose any valid variable name. This variable allows you to access properties and methods of the exception object, such as `Message`, `StackTrace`, and `InnerException`.
	Example:
```c#
try
{
    int result = 10 / 0; // This will throw a DivideByZeroException
}
catch (DivideByZeroException ex) //examples of exception variables
{
    Console.WriteLine("Message: " + ex.Message); // Get the error message 
    Console.WriteLine("StackTrace:\n" + ex.StackTrace); // Get the stack trace 
    Console.WriteLine("HelpLink: " + ex.HelpLink); // Get the help link (if set) 
    Console.WriteLine("Source: " + ex.Source); // Get the source of the exception 
    Console.WriteLine("TargetSite: " + ex.TargetSite); // Get the method that threw the exception
}
```
You can also manually throw an error using `throw new Exception()`.

When throwing an error, these are the three most common exceptions and their parameters:
- ArgumentNullException:
```c#
ArgumentNullException(string paramName, string message);
//paramName Optional
```
sample use of ArgumentNullException:
```c#
public void MyMethod(string input)
{
    if (input == null)
    {
        throw new ArgumentNullException(nameof(input), "Input cannot be null.");
    }

    // Rest of your method logic here
}
```

- ArgumentException:
```c#
public ArgumentException(string message, string paramName, Exception innerException);
//every parameter Optional
```

- Exception (Base Exception):
```c#
Exception(string message, Exception innerException);
//message optional, innerException optional
```
Just use the built in suggestor if you want to know all the exceptions and their parameters.

Custom exceptions can be created, see: [[custom exceptions]]
###### You can also use if else to predict and throw an error. Syntax:
```c#
if (//predicted error)
{
    throw new JustASampleException("manual error message");
}
else
{
    //error not existent or not catched
}
```

when to use **if else** or **try catch** when defending your program?
in general:
- **if/else** is for normal program flow / predictable expected cases.
- **try/catch** to handle abnormal conditions / suspect something can or will go wrong and you don't want it to bring down the whole system, like network timeout/file system access problems, files doesn't exist, etc. Try catching is used for catching the error and preventing problems along the way, its like a checkpoint because code will still run if catch is executed, it will only stop if nothing was caught and something escaped.
### NOTE:
- Try/catch shouldn't be used to protect yourself from bad programming -- the "I don't know what will happen if I do this so I'm going to wrap it in a try/catch and hope for the best" kind of programming. Typically you'll want to restrict the kinds of exceptions you catch to those that are not related to the code itself (server down, bad credentials, etc.) so that you can find and fix errors that are code related (null pointers, etc.).
- code will continue if **catch** is executed, code will stop and throw an unhandled exception if no catch is detected for the exception. 