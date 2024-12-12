**GetMethods()**: You can use the `GetMethods()` method on a `Type` object to retrieve an array of `MethodInfo` objects representing the methods defined in that type.
**GetMethod()**: If you know the name of a specific method you want to work with, you can use the `GetMethod()` method to retrieve a `MethodInfo` object for that method.
Difference between `GetMethod` and `GetMethods` is that GetMethods returns an array of `MethodInfo`, GetMethod returns only one.

syntax GetMethods:
```c#
MethodInfo[] methods = type.GetMethods();
```
syntax GetMethod:
```c#
MethodInfo method = type.GetMethod("MethodName");
```

sample GetMethod:
```c#
class MyClass
{
    public void Method1() { Console.WriteLine("Method1 called"); }
    public void Method2(string message) { Console.WriteLine($"Method2 called with message: {message}"); }
}

class Program
{
    static void Main()
    {
        Type type = typeof(MyClass);

        // Get a specific method by name
        MethodInfo method1 = type.GetMethod("Method1");

        // Create an instance of the class
        MyClass myObject = new MyClass();

        // Invoke the retrieved method
        method1.Invoke(myObject, null); // Method1 called
    }
}
```
sample GetMethods:
```c#
class Program
{
    static void Main()
    {
        Type type = typeof(MyClass);
        MethodInfo[] methods = type.GetMethods();

        Console.WriteLine("Methods in MyClass:");
        foreach (MethodInfo method in methods)
        {
            Console.WriteLine($"Method Name: {method.Name}");
        }
    }
}

class MyClass
{
    public void Method1() { }
    public int Method2() { return 0; }
}
```
Here, we use `GetMethods()` to retrieve and display the methods defined in the `MyClass` type.