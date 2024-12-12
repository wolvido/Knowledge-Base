#cSharp 
basically a python variable where you dont need to set the type just write `name = "name" or name = 1`

syntax:
```c#
dynamic variableName = data;
```

**Dynamic Typing**: When you declare a variable as `dynamic`, the C# compiler defers type checking until runtime. This means you can assign values of any type to a `dynamic` variable without triggering compile-time type errors.
```c#
dynamic dynamicVar = 10; // Assign an integer
dynamicVar = "Hello";   // Assign a string
dynamicVar = new MyClass(); // Assign an instance of a class
```
**Important Note**:  this does not mean that it will not throw an error, if the dynamic variable is fed to something that expects an int, but instead gets a string, it will throw an error.

**Dynamic Casting:** 
- If you use dynamic in a var, var will become dynamic, sample:
```c#
dynamic a = 5;
dynamic b = 5;
var c = a + b; //c is of type dynamic
```
- you can convert a static data type into a dynamic type and vice versa:
```c#
int i = 5;
dynamic d = i;
int x = d;
```
- dynamic also implicitly upcasts if possible:
```c#
int i = 5;
dynamic d = i;
long x = d;
//can also be downcasted
```


**Late Binding**: Operations on `dynamic` variables are resolved at runtime. This allows you to call methods and access properties that may not be known until the program is executing.
```c#
dynamic person = new Person();
string name = person.GetName(); // GetName method does not exist
```

**Interoperability**: `dynamic` is often used when working with dynamic languages, COM objects, or libraries that don't have a static C# type.
```c#
dynamic comObject = GetComObject();
dynamic result = comObject.InvokeMethod("DoSomething");
```

**Reflection**: `dynamic` can be used with reflection to simplify code that interacts with types and members through reflection.
```c#
dynamic instance = Activator.CreateInstance(type);
dynamic result = instance.MethodName();
```
