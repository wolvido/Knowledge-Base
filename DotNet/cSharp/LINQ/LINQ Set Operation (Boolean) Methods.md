#cSharp 
- **SequenceEqual**: Compares two sequences for equality.
- **Any / All**: Determine if any or all elements satisfy a condition.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// SequenceEqual: Compares two sequences for equality
var areEqual = numbers.SequenceEqual(otherNumbers);
Console.WriteLine("Are numbers and otherNumbers equal? " + areEqual);

// Any: Checks if any elements satisfy a condition
var anyEven = numbers.Any(x => x % 2 == 0);
Console.WriteLine("Any Even Numbers: " + anyEven);

// All: Checks if all elements satisfy a condition
var allEven = numbers.All(x => x % 2 == 0);
Console.WriteLine("All Numbers Even: " + allEven);
```