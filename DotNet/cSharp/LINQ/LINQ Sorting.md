#cSharp 
- **OrderBy / OrderByDescending**: Sorts elements in ascending or descending order.
 - **ThenBy / ThenByDescending**: Performs secondary sorting.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// OrderBy / OrderByDescending: Sorts elements in ascending or descending order
var orderedNumbers = numbers.OrderBy(x => x);
Console.WriteLine("Ordered Numbers (Ascending):");
foreach (var number in orderedNumbers)
{
    Console.WriteLine(number);
}

// ThenBy / ThenByDescending: Performs secondary sorting (not shown here)
var sortedThenBy = numbers.OrderBy(num => num)
	.ThenByDescending(num => num); 
Console.WriteLine("\nSorted Numbers (Ascending) Then By (Descending):"); 
foreach (var number in sortedThenBy) 
{ 
	Console.WriteLine(number); 
}
```