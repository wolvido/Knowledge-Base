Limits the data type allowed in the generic, Examples:

#cSharp 
1. **Class Constraint (`where T : class`):** This constraint specifies that `T` must be a reference type (a class, interface, delegate, or array, but not a value type like `int`).
```c#
public class MyClass<T> where T : class
{
    // ...
}
```
2. **Base Class Constraint (`where T : MyBaseClass`):** This constraint specifies that `T` must be or derive from a specific base class. Not to be confused with `class`, `MyBaseClass` is any custom base class.
```c#
public class MyDerivedClass<T> where T : MyBaseClass
{
    // ...
}
```
3. **Struct Constraint (`where T : struct`):** This constraint specifies that `T` must be a value type or a struct.
```c#
public class MyStruct<T> where T : struct
{
    // ...
}
```
4. **Constructor Constraint (`where T : new()`):** Argument T must have a public parameterless constructor, like a class with a default constructor. When used together with other constraints, the `new()` constraint must be specified last. Cannot be combined with the `struct` and `unmanaged` constraints, since it only accepts reference types.
```c#
public class MyConstructor<T> where T : new()
{
    // ...
}
```
You may also need to instantiate T inside a class, if so you need to use new() or it will throw an error. example
```c#
public class Foo<T> where T : new()
{
    public void test()
    {
        var obj = new T(); //will throw if new() is removed
    }
}
```

5. **Interface Constraint (`where T : ISomeInterface`):** This constraint specifies that `T` must implement a specific interface.
```c#
public class MyInterface<T> where T : ISomeInterface
{
    // ...
}
```
6. **Multiple Constraints (`where T : SomeInterface, new()`):** You can combine multiple constraints by separating them with commas.
```c#
public class MyComplexClass<T> where T : ISomeInterface, new()
{
    // ...
}
```
for a full list of constraints see: [Constraints on type parameters](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters)