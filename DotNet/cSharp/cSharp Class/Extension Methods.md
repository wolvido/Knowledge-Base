---
keywords: |-
  extend built in data types
  extend built in class
  extend existing data types
  extend existing class
  add new methods to built in
  add new methods to existing
  this as a parameter
  this as parameter
---
#cSharp 
##### Syntax:
```c#
public static ReturnType ExtensionMethodName(this ExtendedType extendedParameter, additionalParameters)
{
    // Method body
    // Code to implement the extension method
}
```
- `ReturnType`: The return type of the extension method.
- `ExtensionMethodName`: The name of the extension method.
- `ExtendedType`: The data type you want to extend. The `this` keyword is used as a modifier, indicating that this method extends this type.
- `extendedParameter`: The parameter that represents an instance of the extended type on which the extension method can be accessed. Basically it acts as the object. sample:
```c#
DataType sample = "sample"; 
sample.ExtensionMethodName(parameters) //extendedParameter is the sample
```
basically just making a method in a "call" way.
- `additionalParameters`: Any additional parameters required by the extension method.
### Sample:
```c#
public static class StringExtensions
{
    public static string Repeat(this string input, int count) //extending string
    {
        if (count <= 0)
            throw new ArgumentException("Count must be greater than zero.", nameof(count));
            
        return string.Concat(Enumerable.Repeat(input, count));
    }
}

public class Program
{
    public static void Main()
    {
        string text = "Hello, ";
        int repeatCount = 3;
        
        string repeatedText = text.Repeat(repeatCount);
        
        Console.WriteLine($"Original Text: {text}");
        Console.WriteLine($"Repeated Text ({repeatCount} times): {repeatedText}");
    }
}
```
##### Convention:
- extension class name should end with Extensions
##### **Guideline by msdn**:
only create an extension method for a built in type as a last resort since an update on a built in will break your code. Its ok if you are extending a non built in classes.
As an alternative create a derive from the built in types and add your new methods there. If that doesnt work then do it as a last resort.

You can also use extension methods in order to create cleaner looking call methods.
see [[Custom Middleware]] for a sample on how its used.
