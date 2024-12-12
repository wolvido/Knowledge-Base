#cSharp 
Keywords:
	# null reference error on class list
	
Your using null, your trying to use null, maybe a null variable, find where the null is.

Problem: you have a null reference error on a class list. 

Solution: A list field need to be initialized because list is a reference type and its default value is null. Value types are not affected since they have default values.  

When adding a list member or any reference type, instead of making a constructor like this:  
```cSharp
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