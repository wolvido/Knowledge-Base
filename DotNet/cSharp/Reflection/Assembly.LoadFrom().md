**Assembly.LoadFrom()**: To load an assembly, you can use the `Assembly.LoadFrom()` method. This allows you to access types and members within the loaded assembly. Required if reflection is being done on a different assembly.
syntax:
```c#
Assembly assembly = Assembly.LoadFrom("MyLibrary.dll");
```
sample:
```c#
class Program
{
    static void Main()
    {
        Assembly assembly = Assembly.LoadFrom("MyLibrary.dll");

        Console.WriteLine($"Loaded assembly: {assembly.FullName}");
    }
}
```
This code loads an assembly named "MyLibrary.dll" using `Assembly.LoadFrom()`.