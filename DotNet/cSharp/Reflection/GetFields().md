**GetFields()**: The `GetFields()` method allows you to retrieve an array of `FieldInfo` objects representing the fields (variables) defined in a type.
syntax:
```c#
FieldInfo[] fields = type.GetFields();
```
sample:
```c#
class Program
{
    static void Main()
    {
        Type type = typeof(MyClass);
        FieldInfo[] fields = type.GetFields();

        Console.WriteLine("Fields in MyClass:");
        foreach (FieldInfo field in fields)
        {
            Console.WriteLine($"Field Name: {field.Name}");
        }
    }
}

class MyClass
{
    public int Age;
    public string Name;
}
```
In this sample, `GetFields()` is used to retrieve and display the fields defined in the `MyClass` type.