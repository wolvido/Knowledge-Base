keywords:
	reference vs value type

#cSharp 
![[Pasted image 20230726133923.png]]
value types sources data from itself  
a reference type contains only the reference pointing/sourcing to a separate variable stored in the stack.  
  
- if you create a copy of a value type, you create another variable that is different from the original.  
- if you create a copy of a reference type, you create a copy of the reference pointing to a separate variable stored in the stack. The source variable stays the same and is not copied.  
  
- If you modify the copy of a value type, it does not affect the original since they are separate variables.  
- If you modify the copy of a reference type, you also modify the original reference type since the original and the copy of the reference type sources/points to the same edited variable.
#### sample:
```c#
class Person //class is a reference type
{  
	public string Name { get; set; }  
}
  
Person person1 = new Person { Name = "Alice" };  
Person person2 = person1; // Both person1 and person2 now refer to the same object  
  
person2.Name = "Bob"; // Changes the object's Name property through person2  
Console.WriteLine(person1.Name); // Output: Bob, since both variables refer to the same object
```
- integers and structures are value types
- strings and classes are reference types
# Warning
- **what**: Contains(), Equals() method and == keyword compare by reference, not by value. see: [#402 – Value Equality vs. Reference Equality | 2,000 Things You Should Know About C# (2000things.com)](https://csharp.2000things.com/2011/09/01/402-value-equality-vs-reference-equality/) and Contains implements equals.
- **What to do**: If you compare your object using equals or contains, you need to override them to compare the individual properties or you can implement `IEquatable` . [Generate C# Equals and GetHashCode Method Overrides - Visual Studio (Windows) | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/ide/reference/generate-equals-gethashcode-methods?view=vs-2022). When you override Equals method, it also affects Contains method because Contains implements Equals.
Sample:
```c#
1. public class MyClass : IEquatable<MyClass>
2. {
3.     public int Id { get; set; }
4.     public string Name { get; set; }

5.     //implement IEquatable.Equals() method
6.     public bool Equals(MyClass other)
7.     {
8.         if (other == null)
9.         {
10.             return false;
11.         }

12.         return Id == other.Id && Name == other.Name;
13.     }
14. }

15. var obj1 = new MyClass { Id = 1, Name = "John" };
16. var obj2 = new MyClass { Id = 1, Name = "John" };

17. if (obj1.Equals(obj2)) //it calls MyClass.Equals() method
18. {
19.     Console.WriteLine("The two objects are equal.");
20. }
21. else
22. {
23.     Console.WriteLine("The two objects are not equal.");
24. }
25. //Output: The two objects are equal.
```
