---
keywords: how to add documentation to codes
---
Allows you to document your code.
#### How-to:
On top of your method or class type triple slash `///`
this will generate xml documentation comments.
sample:
```c#
/// <summary>
/// Represents a simple calculator class.
/// </summary>
public class Calculator
{
    /// <summary>
    /// Adds two integers and returns the result.
    /// </summary>
    /// <param name="a">The first integer.</param>
    /// <param name="b">The second integer.</param>
    /// <returns>The sum of the two integers.</returns>
    public int Add(int a, int b)
    {
        return a + b;
    }
}
```
When you use the `Calculator.Add` method somewhere else, if you hover the mouse on the method, intellisence will automatically provide info similar to how native .net methods and classes provide info.
