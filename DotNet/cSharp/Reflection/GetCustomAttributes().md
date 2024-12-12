**GetCustomAttributes()**: This method allows you to retrieve an array of custom attributes applied to a type, method, property, or other member.
syntax:
```c#
MyCustomAttribute[] attributes = (MyCustomAttribute[])type.GetCustomAttributes(typeof(MyCustomAttribute), false);
```
sample:
```c#
[MyCustom("Custom Description")]
class MyClass
{
}

[AttributeUsage(AttributeTargets.Class, Inherited = false, AllowMultiple = false)]
sealed class MyCustomAttribute : Attribute
{
    public string Description { get; }

    public MyCustomAttribute(string description)
    {
        Description = description;
    }
}

class Program
{
    static void Main()
    {
        Type type = typeof(MyClass);
        MyCustomAttribute[] attributes = (MyCustomAttribute[])type.GetCustomAttributes(typeof(MyCustomAttribute), false);

        foreach (MyCustomAttribute attribute in attributes)
        {
            Console.WriteLine($"Custom Attribute Description: {attribute.Description}");
        }
    }
}
```
In this example, `GetCustomAttributes()` is used to retrieve and display custom attributes applied to the `MyClass` type.