#cSharp 
1. **Where**: Filters elements based on a specified condition.
2. **Select**: Transforms elements each element into a new result.
3. **SelectMany**: Projects elements and flattens the result.
4. **OfType**: Filters elements based on their type.
5. **Cast**: Casts elements to a specified type.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Where: Filters elements based on a specified condition
var evenNumbers = numbers.Where(x => x % 2 == 0);
Console.WriteLine("Even Numbers:");
foreach (var number in evenNumbers)
{
	Console.WriteLine(number);
}

// Select: Projects or transforms elements into a new shape
var squaredNumbers = numbers.Select(x => x * x);
Console.WriteLine("Squared Numbers:");
foreach (var number in squaredNumbers)
{
	Console.WriteLine(number);
}

// SelectMany: Projects elements and flattens the result (not shown here)
var combinedNumbers = numbers.SelectMany(num => otherNumbers, (num1, num2) => num1 * num2); Console.WriteLine("Combined Numbers:");
foreach (var number in combinedNumbers)
{
	Console.WriteLine(number);
}

// OfType: Filters elements based on their type
var onlyIntegers = numbers.OfType<int>();
Console.WriteLine("Only Integers:");
foreach (var number in onlyIntegers)
{
	Console.WriteLine(number);
}

// Cast: Casts elements to a specified type
var castToInt = numbers.Cast<int>();
Console.WriteLine("Casted to Integers:");
foreach (var number in castToInt)
{
	Console.WriteLine(number);
}
