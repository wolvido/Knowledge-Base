#cSharp 
- **Take**: Returns a specified number of elements from the beginning of a sequence.
- **Skip**: Skips a specified number of elements from the beginning of a sequence.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Take: Returns a specified number of elements from the beginning of a sequence
var firstThree = numbers.Take(3);
Console.WriteLine("First Three Numbers:");
foreach (var number in firstThree)
{
    Console.WriteLine(number);
}

// Skip: Skips a specified number of elements from the beginning of a sequence
var skipTwo = numbers.Skip(2);
Console.WriteLine("After Skipping Two Numbers:");
foreach (var number in skipTwo)
{
    Console.WriteLine(number);
}
```