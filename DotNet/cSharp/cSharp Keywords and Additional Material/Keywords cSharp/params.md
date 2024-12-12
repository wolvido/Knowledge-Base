#cSharp 
keywords:
	-easier ways to make methods  
	-better ways to make methods  
	-method accept arrays  
	-constructors accept arrays

Instead of creating overloads for every data with the same type, use params.

example:
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
//etc..
```
instead of the example above, you can use:
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