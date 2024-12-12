[[params]] | [[Knowledge Base/DotNet/cSharp/cSharp Keywords and Additional Material/generic]]
#cSharp 
keywords:
	# c# class methods  
	# c# parts of a method  
	# c# parts of a class method
	# cSharp class methods  
	# cSharp parts of a method  
	# cSharp parts of a class method

Method Declarations  
syntax:  
```c#
[access modifier] [modifier optional] return-type MethodName([parameters])  
{  
	// Method body  
}
```
example:
```c#
public static int AddNumbers(int a, int b)  
{
	int sum = a + b;
	return sum;
}
```
**Access modifier/Accessibility**: includes public, private, protected, and internal. They determine where the method can be accessed from within the program.  
  
**Modifier optional**: They modify the behavior or characteristics of the method. Include static, virtual, abstract, override, and sealed. Modifiers are optional.  
  
**Return Type**: It indicates the type of value that the method returns after executing its operations. It can be any valid C# data type, including custom types or void if the method doesn't return any value.  
  
**Method Name**: It is the name given to the method, which is used to identify and call the method within the program. Method names should follow naming conventions and should be descriptive of the functionality they provide.  
  
**Parameters**: They represent the inputs or data that can be passed to the method. Parameters are enclosed within parentheses () and separated by commas ,. Each parameter consists of a data type and a name. They allow values to be passed into the method for processing.  
  
**Method Body**: It contains the actual code or statements that define the operations to be performed by the method. The method body is enclosed within curly braces {} and includes the set of instructions executed when the method is called.

***see [[Modifiers]] for more list of modifiers.***

#### Things to remember:
##### [[params]]:  
Instead of creating overloads for every data with the same type, use [[params]] in methods.
ex:
```c#
public int CalculateSum(int num1)  
{  
	return num1;  
}  
public int CalculateSum(int num1, int num2)  
{  
	return num1 + num2;  
}  
public int CalculateSum(int num1, int num2, int num3)  
{  
	return num1 + num2 + num3;  
}
//etc...
```
instead of the example above, you can use params:
```c#
public int CalculateSum(params int[] numbers)  
{  
	int sum = 0;  
	foreach (int num in numbers)  
	{  
		sum += num;  
	}  
	return sum;  
}
```
##### [[Knowledge Base/DotNet/cSharp/cSharp Keywords and Additional Material/generic]]:
-if you need a method that can be used on any data type, use [[Knowledge Base/DotNet/cSharp/cSharp Keywords and Additional Material/generic]]. Like for example you have a method that can add two int, you can also configure that method to add two strings instead of creating another one to add strings.