#cSharp 
**GetType()**: You can use the `GetType()` method on an object to get a reference to its `Type` object. This is often used when you have an instance of an object and want to inspect its type.
syntax:
```c#
Type type = myObject.GetType();
```
sample:
```c#
class Program
{
    static void Main()
    {
        object myObject = new MyClass();
        Type type = myObject.GetType();

        Console.WriteLine($"Type of myObject: {type.FullName}");
    }
}

class MyClass
{
}
```
In this sample, we use `GetType()` to get the type of an object (`MyClass`) dynamically.