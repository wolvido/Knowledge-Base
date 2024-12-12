---
keywords: code reading code
---
#cSharp 
"Reflection" is the way in which we can turn the very code we write into _data_. Or you could say that "reflection" is how code can look at _itself_ (like the reflection of a mirror).

With reflection, I can look at a `Type` instance of a class and get collections of information about that class like a collection of properties, methods, and other members as well as attributes that the class was tagged with. Further, I can even invoke members on an instance of a class using reflection without having to write statically typed code.

Reflection is extremely powerful but it is slow and can be easily abused. By using reflection, we are foregoing the protection of our compiler. For example, suppose I write some code that reflects on instances of `MyClass` to invoke the parameterless method `Run()`. If I later rename the method as `Execute()`, I'll have to _know_ to also change the code using reflection since we have to use strings to specify specific members of a type, strings that things like compilers and intellisense won't assume are related to the name of members on a class. This means that you'll catch bugs in your reflection code only during runtime and not during compilation/build. At this point, you'd need to write unit tests specifically to catch these issues for you but this indirection isn't something we want for _most_ scenarios.

**How do we do reflection?**
To use reflection in C#, you will use a combination of methods and properties provided by the `Type` class (from the `System.Reflection` namespace) to inspect and interact with types and their members. Here are some commonly used methods and properties for reflection:

1. **GetType()**: You can use the `GetType()` method on an object to get a reference to its `Type` object. This is often used when you have an instance of an object and want to inspect its type.
see: [[GetType()]]

2. **Assembly.LoadFrom()**: To load an assembly, you can use the `Assembly.LoadFrom()` method. This allows you to access types and members within the loaded assembly. Required if reflection is being done on a different assembly.
see: [[Assembly.LoadFrom()]]

3. **GetMethods()**: You can use the `GetMethods()` method on a `Type` object to retrieve an array of `MethodInfo` objects representing the methods defined in that type.
see: [[GetMethod() GetMethods()]]

4. **GetProperties()**: Similarly, you can use the `GetProperties()` method to retrieve an array of `PropertyInfo` objects representing the properties of a type.
see: [[GetPropertie() GetProperties()]]

5. **GetFields()**: The `GetFields()` method allows you to retrieve an array of `FieldInfo` objects representing the fields (variables) defined in a type.
see: [[GetFields()]]

6. **GetEvents()**: You can use the `GetEvents()` method to retrieve an array of `EventInfo` objects representing the events defined in a type.
see: [[GetEvents()]]

7. **GetCustomAttributes()**: This method allows you to retrieve an array of custom attributes applied to a type, method, property, or other member.
see: [[GetCustomAttributes()]]

8. **GetMethod()**: If you know the name of a specific method you want to work with, you can use the `GetMethod()` method to retrieve a `MethodInfo` object for that method.
see: [[GetMethod() GetMethods()]]

9. **GetProperty()**: Similarly, you can use the `GetProperty()` method to retrieve a `PropertyInfo` object for a specific property.
see: [[GetPropertie() GetProperties()]]

These are just a few of the methods and properties provided by the `Type` class and other reflection-related classes. You can use them based on your specific needs when working with reflection in C#.
