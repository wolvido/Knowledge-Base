#cSharp 
- **ToList**: Converts a sequence into a list.
- **ToArray**: Converts a sequence into an array.
- **ToDictionary**: Converts a sequence into a dictionary.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// ToList: Converts a sequence into a list
var listNumbers = numbers.ToList();
Console.WriteLine("List of Numbers:");
foreach (var number in listNumbers)
{
    Console.WriteLine(number);
}

// ToArray: Converts a sequence into an array
var arrayNumbers = numbers.ToArray();
Console.WriteLine("Array of Numbers:");
foreach (var number in arrayNumbers)
{
    Console.WriteLine(number);
}

// ToDictionary: Converts a sequence into a dictionary
var dictNumbers = numbers.ToDictionary(x => x, x => $"Value {x}");
Console.WriteLine("Dictionary of Numbers:");
foreach (var kvp in dictNumbers)
{
    Console.WriteLine($"Key: {kvp.Key}, Value: {kvp.Value}");
}
```