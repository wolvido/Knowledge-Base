#cSharp 
- **Any**: Checks if any elements satisfy a condition.
- **All**: Checks if all elements satisfy a condition.
- **Contains**: Checks if a sequence contains a specified element.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Any: Checks if any elements satisfy a condition
var anyEven = numbers.Any(x => x % 2 == 0);
Console.WriteLine("Any Even Numbers: " + anyEven);

// All: Checks if all elements satisfy a condition
var allEven = numbers.All(x => x % 2 == 0);
Console.WriteLine("All Numbers Even: " + allEven);

// Contains: Checks if a sequence contains a specified element
var containsValue = numbers.Contains(3);
Console.WriteLine("Contains Value 3: " + containsValue);
```