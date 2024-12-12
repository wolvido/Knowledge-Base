#cSharp 
- **Distinct**: Returns distinct elements from a sequence.
- **Union**: Combines two sequences, returning unique elements.
- **Intersect**: Returns elements that appear in both sequences.
- **Except**: Returns elements that appear in the first sequence but not in the second.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Distinct: Returns distinct elements from a sequence
var distinctNumbers = numbers.Distinct();
Console.WriteLine("Distinct Numbers:");
foreach (var number in distinctNumbers)
{
    Console.WriteLine(number);
}

// Union: Combines two sequences, returning unique elements
var unionNumbers = numbers.Union(otherNumbers);
Console.WriteLine("Union of Numbers:");
foreach (var number in unionNumbers)
{
    Console.WriteLine(number);
}

// Intersect: Returns elements that appear in both sequences
var intersectNumbers = numbers.Intersect(otherNumbers);
Console.WriteLine("Intersection of Numbers:");
foreach (var number in intersectNumbers)
{
    Console.WriteLine(number);
}

// Except: Returns elements that appear in the first sequence but not in the second
var exceptNumbers = numbers.Except(otherNumbers);
Console.WriteLine("Numbers not in 'otherNumbers':");
foreach (var number in exceptNumbers)
{
    Console.WriteLine(number);
}