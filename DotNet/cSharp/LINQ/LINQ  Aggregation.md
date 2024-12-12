#cSharp 
- **Count**: Counts the number of elements in a sequence.
- **Sum**: Calculates the sum of numeric elements.
- **Min**: Finds the minimum element.
- **Max**: Finds the maximum element.
- **Average**: Computes the average of numeric elements.
- **Aggregate**: Applies an accumulator function over a sequence.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Count: Counts the number of elements in a sequence
var count = numbers.Count();
Console.WriteLine("Count of Numbers: " + count);

// Sum: Calculates the sum of numeric elements
var sum = numbers.Sum();
Console.WriteLine("Sum of Numbers: " + sum);

// Min: Finds the minimum element
var min = numbers.Min();
Console.WriteLine("Minimum Number: " + min);

// Max: Finds the maximum element
var max = numbers.Max();
Console.WriteLine("Maximum Number: " + max);

// Average: Computes the average of numeric elements
var average = numbers.Average();
Console.WriteLine("Average of Numbers: " + average);

// Aggregate: Applies an accumulator function over a sequence 
var product = numbers.Aggregate((acc, num) => acc * num); 
Console.WriteLine("Product of Numbers: " + product);
```
