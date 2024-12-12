#cSharp 
keywords:
	method with switchable data types
	method for varying data types
	method with varying data types
	replaceable data type
	replaceble data type //its meant to be a typo
	method with switchable datatypes
	method for varying datatypes
	method with varying datatypes
	replaceable datatype
	replaceble data type //its meant to be a typo
	method that can handle multiple data type
	method that can handle multiple datatype
	class with switchable data types
	class for varying data types
	class with varying data types
	replaceable data type
	replaceble data type //its meant to be a typo
	class with switchable datatypes
	class for varying datatypes
	class with varying datatypes
	replaceable datatype
	replaceble data type //its meant to be a typo
	class that can handle multiple data type
	class that can handle multiple datatype
	interface with switchable data types
	interface for varying data types
	interface with varying data types
	replaceable data type
	replaceble data type //its meant to be a typo
	interface with switchable datatypes
	interface for varying datatypes
	interface with varying datatypes
	replaceable datatype
	replaceble data type //its meant to be a typo
	interface that can handle multiple data type
	interface that can handle multiple datatype
	store multiple datatypes
Essentially, in a class or a method, the parameters are objects (the ones inside the parenthesis() of a method).
Generic is a way for a class or a method to accept a Type instead of an object, it will be inside arrow keys <>.

Let's say we need to have a class that has two integer numbers, and a method that prints those two numbers with a plus sign between them. Something like this:
```c#
public class Foo  
{  
	public int A { get; set; }  
	public int B { get; set; }  
	public void Sum()  
	{  
		Console.WriteLine($"{A}+{B}");  //just an example, it doesnt sum it just outputs "10+20" not 30
	}  
}
```
Simple right? But what if we wanted the same kind of class but for decimal numbers? So we make a copy of that class, replacing every int with decimal. 
But now the client says he wants the same for long and for double and for string. Things are getting out of hand now!

Wouldn't it be nice if we told the computer instead of int that it could expect any kind of type (without breaking strong typing)? Generics to the rescue!
```c#
public class Foo<T>  
{  
	public T A { get; set; }  
	public T B { get; set; }  
	public void Sum()  
	{  
		Console.WriteLine($"{A}+{B}");  
	}  
}
```
Here T is a placeholder for any type. It could be int, long, string, even a custom class you created. You use it like this:
```c#
var x = new Foo<int>;  
var y = new Foo<decimal>;  
var z = new Foo<string>;
```
There is more stuff you could do. You can for instance constrict what kind of T your class accepts, and you can change the logic inside the class depending on what kind of T you have.
**Note:** T is a convention, it means Type. The convention is to add a T to the front of your generic parameter like TCustomType, like how they add I on interface.

You can also limit what T data type a generic will allow using [[Generic Constraints]]
### Generic also works in other types like:
#### Generic On method:
```c#
// Generic method to find the minimum value in an array
static T FindMin<T>(T[] array) where T : IComparable<T>
{
	if (array == null || array.Length == 0)
	{
		throw new ArgumentException("Array must not be empty or null");
	}
	T min = array[0];
	
	for (int i = 1; i < array.Length; i++)
	{
		if (array[i].CompareTo(min) < 0)
		{
			min = array[i];
		}
	}
	return min;
}
```
#### Generic On Interfaces:
```c#
public interface IGenericInterface<T> 
{ 
	void PrintData(T data); 
}
```
#### And of course a Class:
```c#
public class GenericClass<T>
{
    private T _data;

    public GenericClass(T data) //initialize generic data in the _data field
    {
        _data = data; 
    }

    public T GetData() //return the generic data
    {
        return _data; 
    }
}
```

Basically data type injection; can be used for loose coupling.