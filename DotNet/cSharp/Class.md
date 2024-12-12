#cSharp
links and related:
	[[Abstract class]] | [[casting]] | [[class indexer]] | [[class valid state]] | [[Composition]] | [[constructor]] | [[Delegate]] | [[fields]] | [[Generic]] | [[Inheritance]] | [[Interface]] | [[method]] | [[Method Overriding]] | [[Modifiers]] | [[object initializer]] | [[private fields]] | [[properties]] | [[Static class]] | [[Struct]] | [[When to use coupling vs inheritance]] | 

Here's a basic example of a class in C#:
```c#
public class MyClass  
{  
	// Fields  
	private int _myField;  

	// Constructor  
	public MyClass(int myField)  
	{  
		_myField = myField;  
	}  
	
	// Properties  
	public int MyProperty  
	{  
		get { return myField; }  
		set { myField = value; }  
	}  
	
	// Methods  
	public void MyMethod()  
	{  
		// Method implementation  
	}  
	
	// Static Methods  
	public static void StaticMethod()  
	{  
		// Method implementation  
	}  
}
```
  
To use the class:  
```c#
MyClass myObject = new MyClass();  
myObject.MyProperty = 42;  
myObject.MyMethod();  
myObject.StaticMethod();  
```

see [[constructor]] note for more details and best practices
see [[properties]] note for more details and best practice
  
Things to remember:  
- class should always be in a [[class valid state]]. see class valid state note for more details.  
- fields should be underlined and camelcase ex:  ```_testField ``` see: [[Naming Convention]]
- Do not allow fields to be modified by outside without properties or methods, fields are not to be exposed. see [Why Properties Matter (csharpindepth.com)](https://csharpindepth.com/Articles/PropertiesMatter)
- you can create multiple constructors for overload. like constructors for default parameters or full parameters or half.  see: [[Overload]]
- you can use read only if you think a field will not or should not be change after initialization, even internally. read only can only be change in initialization and construction. see [[Modifiers]] read only section for more info.
- If you need a class that will hold a collection of data, you can create custom indexers within a class like a dictionary or a list, specifying how objects of that class can be accessed using index notation like so:
``` c#
class["key"] = "answer";  
Console.Writeline(class["key"]); //will return "answer"  
```
see [[class indexer]] note.  
- a list field needs to be initialized because list is a reference type and its default value is null. Value types are not affected since they have default values.  
when adding a list member or any reference type, instead of making a constructor like this:  
``` c#
public List<string> Test;  
public Constructor()  
{  
	this.Test = new List<string>();  
}  
```
you can initialize it in the **field** section of the class like this:  
```c#
public List<string> Test = new List<string>(); //no need to make a constructor
public List<string> Test = new(); //use this for even simpler sugar
```
- if you need a class that can be used on multiple data type, use [[Knowledge Base/DotNet/cSharp/cSharp Keywords and Additional Material/generic]]. For example you want a class to be able to add an int but also when needed that class can also add strings without calling extra methods. Simply switching the data type parameter.
- Utilize [[Interface]] or [[Delegate]] they are the holy grail of oop.
- If you want to add methods to some built in class and data types, use [[Extension Methods]].
- consider using [[Struct]] instead of class for small data-centric types that provide little or no behavior.

**The thing that you should never forget:**
- you can pass an object into another object. see: [[you can pass an object into another object]]
