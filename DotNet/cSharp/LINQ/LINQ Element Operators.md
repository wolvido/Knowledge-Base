#cSharp 
- **First / FirstOrDefault**: Returns the first element that satisfies a condition if none then the default value.
- **Last / LastOrDefault**: Returns the last element that satisfies a condition if none then or the default value.
- **Single / SingleOrDefault**: Returns a single element that satisfies a condition if none then or the default value.
- **ElementAt / ElementAtOrDefault**: Returns an element at a specified index if none then or the default value.
**Note**: the default prevents errors by returning null.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// First / FirstOrDefault: Returns the first element that satisfies a condition if none then the default value
var firstEven = numbers.First(x => x % 2 == 0);
Console.WriteLine("First Even Number: " + firstEven);

// Last / LastOrDefault: Returns the last element that satisfies a condition if none then or the default value
var lastOdd = numbers.Last(x => x % 2 != 0);
Console.WriteLine("Last Odd Number: " + lastOdd);

// Single / SingleOrDefault: Returns a single element that satisfies a condition if none then or the default value
var singleValue = numbers.Single(x => x == 3);
Console.WriteLine("Single Value (3): " + singleValue);

// ElementAt / ElementAtOrDefault: Returns an element at a specified index if none then or the default value
var elementAtIndex2 = numbers.ElementAt(2);
Console.WriteLine("Element at Index 2: " + elementAtIndex2);
```