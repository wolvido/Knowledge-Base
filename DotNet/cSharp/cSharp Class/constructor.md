#cSharp 
Keywords:
	- c# what is a class constructor  
	purpose of a constructor
>[!info]
>primary constructors have been released and it might be better or not idk, but check it out.
>[Declare and use C# primary constructors in classes and structs | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/primary-constructors)
##### Syntax:
```c#
public class MyClass { 
	// Fields, properties, and methods can be defined here 
	public MyClass() // Constructor 
	{ 
		// Constructor code goes here 
	} 
}
```
It constructs the class, and encapsulates the necessary data.  
- Why is it necessary? what's the point of a constructor? 
	- it is to automate constructing the class, to set the initial state of an object, allocate resources, and perform any necessary setup. See [[private fields]] for eli5 explanation. 
	- Basically if the class is a method then thats the code of the method, thats why its the same name as the class.
- If there's nothing to be constructed, you don't need a constructor. It will automatically make one behind the code.
##### Rule of Thumb:  
1. If it's required to make the class work right, it should be a constructor parameter.  
2. If changing it would break the class, it should be a constructor parameter.  
3. If it's optional, has a sane default, and/or simply and safely changes how the class behaves, it should be an object initializer.  
- As much as possible only create a constructor for data that is crucial for the objects purpose before the object is created and reduce the use of overload. This is to prevent clutter. Additional data can simply be added later.  
- Do not initialize additional data outside of the class every time you create an object. If you find yourself initializing additional data after initializing a class, create a constructor and automate all initialization on the constructor, that's what the constructor is for.  
- if you have a default constructor with no parameters, you can use : this() to apply the default constructor to all overloads like:  
```c#
public Post() //default constructor  
{  
	_dateTime = DateTime.Now;  
}  
public Post(string title, string description) //overload constructor  
: this()  
{  
Title = title;  
Description = description;  
}  
```
Warning: only use : this() on default constructors, using multiple this on many overloads will make the code hard to maintain.  

**Constructor Inheritance**: Constructors are not inherited but you don't have to rewrite the base constructor on the inherited, just call `base()` it acts like the base constructor. Its basically a method that runs the base constructor inside the child's constructor.
```c#
public class Car : Vehicle
{
    public Car(string brand, int year, int doors)
        : base(brand, year)
    {
        NumberOfDoors = doors;
    }
    // ...
}
```
see: [[Inheritance]] for more details.
##### Note:  
- constructors can have overloads. see [[Overload]].
- creating too many optional overloads is not advisable, instead you can add optional data later using object initializers. Having said that, overloads are still extremely useful, it's up to you to decide how to make the class easier to use.    
- a list field needs to be initialized because list is a reference type and its default value is null. Value types are not affected since they have default values.  
when adding a list member or any reference type, instead of making a constructor like this: 
```c#
public List<string> Test;  
public Class()  
{  
this.Test = new List<string>();  
}  
```
you can initialize it in the field section instead like this:  
```c#
public List<string> Test = new List<string>();  
```
no need to make a constructor.

**Questions:**
- the class and the constructor modifier should they be the same? 
	no, they can be different, sometimes you need a protected constructor so it cant be accessed by sub classes or a private constructor to prevent the class from being instantiated and essentially becoming a static class only.
- Why is it necessary? what's the point of a constructor? 
	it is to automate constructing the class, to set the initial state of an object, allocate resources, and perform any necessary setup. See [[private fields]] for eli5 explanation.
- Isn't it redundant that the class name needs to be retyped as the constructor?  
	It is a design choice by C# designers. The main reason for using the class name as the constructor identifier is to explicitly indicate that the method is a constructor and not a regular method.