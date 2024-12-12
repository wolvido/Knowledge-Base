#cSharp 
- **Reverse**: Reverses the order of elements in a sequence.
- **Concat**: Concatenates two sequences.
- **DefaultIfEmpty**: Provides a default value if a sequence is empty.
- **Empty**: Creates an empty sequence.
- **Repeat**: Repeats a sequence a specified number of times.

```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Reverse: Reverses the order of elements in a sequence
var reversedNumbers = numbers.Reverse();
Console.WriteLine("Reversed Numbers:");
foreach (var number in reversedNumbers)
{
    Console.WriteLine(number);
}

// Concat: Concatenates two sequences
var concatenatedNumbers = numbers.Concat(otherNumbers);
Console.WriteLine("Concatenated Numbers:");
foreach (var number in concatenatedNumbers)
{
    Console.WriteLine(number);
}

// DefaultIfEmpty: Provides a default value if a sequence is empty
var emptyList = new List<int>();
var defaultIfEmpty = emptyList.DefaultIfEmpty(42); // Default value is 42
Console.WriteLine("Default If Empty List:");
foreach (var number in defaultIfEmpty)
{
    Console.WriteLine(number);
}

// Empty: Creates an empty sequence
var emptySequence = Enumerable.Empty<int>();
Console.WriteLine("Empty Sequence:");
foreach (var number in emptySequence)
{
    Console.WriteLine(number);
}

// Repeat: Repeats a sequence a specified number of times
var repeatedNumbers = Enumerable.Repeat(10, 3); // Repeat 10, 3 times
Console.WriteLine("Repeated Numbers:");
foreach (var number in repeatedNumbers)
{
    Console.WriteLine(number);
}
```