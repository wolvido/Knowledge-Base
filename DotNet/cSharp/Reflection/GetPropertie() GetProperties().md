#cSharp 
**GetProperties()**: Similarly, you can use the `GetProperties()` method to retrieve an array of `PropertyInfo` objects representing the properties of a type.
**GetProperty()**: Similarly, you can use the `GetProperty()` method to retrieve a `PropertyInfo` object for a specific property.
Difference between `GetProperty` and `GetProperties` is that GetProperties returns an array of `PropertyInfo`, GetProperty returns only one.

syntax GetProperties:
```c#
PropertyInfo[] properties = type.GetProperties();
```
syntax GetProperty:
```c#
PropertyInfo property = type.GetProperty("PropertyName");
```
sample GetProperty:
```c#
class MyClass
{
    public int MyProperty { get; set; } = 42;
}

class Program
{
    static void Main()
    {
        Type type = typeof(MyClass);

        // Get a specific property by name
        PropertyInfo property = type.GetProperty("MyProperty");

        // Create an instance of the class
        MyClass myObject = new MyClass();

        // Get the value of the retrieved property
        int propertyValue = (int)property.GetValue(myObject);

        Console.WriteLine($"Property Value: {propertyValue}"); // Property Value: 42
    }
}
```
sample GetProperties:
```c#
class Program
{
    static void Main()
    {
        Type type = typeof(MyClass);
        PropertyInfo[] properties = type.GetProperties();

        Console.WriteLine("Properties in MyClass:");
        foreach (PropertyInfo property in properties)
        {
            Console.WriteLine($"Property Name: {property.Name}");
        }
    }
}

class MyClass
{
    public int Age { get; set; }
    public string Name { get; set; }
}
```
This code uses `GetProperties()` to retrieve and display the properties defined in the `MyClass` type.