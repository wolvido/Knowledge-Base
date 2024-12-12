#cSharp 
Keywords:
	-Get type in C#
	-C# typeof vs. GetType
	-C# determine object type
	-C# check data type
	-C# get object type
	-C# check variable type
	-C# typeof keyword explained
	-C# GetType() method usage
	-C# is operator for type checking
	-C# type identification methods
	-C# how to retrieve object type
	-C# how to get data type
	-C# how to get datatype

typeof:
```c#
Type type1 = typeof(int); // type1 Output: Int32
Type type2 = typeof(string); // type2 Output: String
```
GetType:
```c#
object myObj = "Hello"; 
Type objectType = myObj.GetType(); // objectType Output: String
```
is:
``` c#
object myObj = "Hello";

if (myObj is string)
{
	Console.WriteLine("myObj is a string.");
}
else
{
	Console.WriteLine("myObj is not a string.");
}
```