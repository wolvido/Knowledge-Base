#cSharp 
allows to query collections, databases, XML, and other data sources using a unified and expressive syntax in C# . 
Methods to help query data, it works on all collection data (all common industry atleast).
#### How it works?
Basically a LINQ Method uses lambda to evaluate each item of the collection. [[Lambda]].
Each item of the collection will be set as the parameter/s of the lambda.
See [[Lambda]] first if you're confused.
#### Method Syntax
sample:
```c#
List<Person> people = new List<Person>
{
    new Person { Name = "Alice", Age = 30 },
    new Person { Name = "Bob", Age = 25 },
    new Person { Name = "Charlie", Age = 35 },
    new Person { Name = "David", Age = 28 },
};

// Filtering older than 30 .Where()
var olderThan30 = people.Where(person => person.Age > 30);
foreach (var person in olderThan30)
{
    Console.WriteLine($"{person.Name} is older than 30.");
}

// select name only .Select()
var names = people.Select(person => person.Name);
foreach (var name in names)
{
    Console.WriteLine($"Name: {name}");
}

// Sorting by age .OrderBy()
var sortedByAge = people.OrderByDescending(person => person.Age);
foreach (var person in sortedByAge)
{
    Console.WriteLine($"{person.Name}, Age: {person.Age}");
}
```
Chaining multiple methods is also allowed, sample:
```c#
// Chaining LINQ methods
//where people is older than 30, select name only, and sort by age
var result = people 
	.Where(person => person.Age > 30) //where people is older than 30
	.Select(person => person.Name) //select name only
	.OrderByDescending(person => person.Age); //and sort by age
		//you can stack another where or another select if need be
	
	foreach (var name in result) 
	{ 
	Console.WriteLine($"Name: {name}"); 
	}
```
The samples above demonstrated **Method Syntax** where you chain methods instead.
There is another method called **Query Syntax**.
#### Query Syntax
If we convert the sample above into query syntax:
```C#
List<Person> people = new List<Person>
{
    new Person { Name = "Alice", Age = 30 },
    new Person { Name = "Bob", Age = 25 },
    new Person { Name = "Charlie", Age = 35 },
    new Person { Name = "David", Age = 28 },
};

// Filtering older than 30 using query syntax
var olderThan30 = from person in people
                  where person.Age > 30
                  select person;
foreach (var person in olderThan30)
{
    Console.WriteLine($"{person.Name} is older than 30.");
}

// Selecting names only using query syntax
var names = from person in people
            select person.Name;
foreach (var name in names)
{
    Console.WriteLine($"Name: {name}");
}

// Sorting by age using orderby query syntax
var sortedByAge = from person in people
                  orderby person.Age descending
                  select person;
foreach (var person in sortedByAge)
{
    Console.WriteLine($"{person.Name}, Age: {person.Age}");
}

// Query syntax chain
var result = from person in people
			 where person.Age > 30
			 orderby person.Age descending
			 select person.Name;
			
foreach (var name in result)
{
	Console.WriteLine($"Name: {name}");
}
```
### All LINQ methods:
##### Filtering and Projection/Selecting:
1. **Where**: Filters elements based on a specified condition.
2. **Select**: Projects or transforms elements into a new shape.
3. **SelectMany**: Projects elements and flattens the result.
4. **OfType**: Filters elements based on their type.
5. **Cast**: Casts elements to a specified type.
see [[LINQ Filtering and Projection-Selecting]] for samples.
##### Sorting:
6. **OrderBy / OrderByDescending**: Sorts elements in ascending or descending order.
7. **ThenBy / ThenByDescending**: Performs secondary sorting.
see [[LINQ Sorting]] for samples.
##### Set Operations (set as in {}):
8. **Distinct**: Returns distinct elements from a sequence.
9. **Union**: Combines two sequences, returning unique elements.
10. **Intersect**: Returns elements that appear in both sequences.
11. **Except**: Returns elements that appear in the first sequence but not in the second.
see [[Set Operations (set as in {})]] for samples
##### Element Operators:
12. **First / FirstOrDefault**: Returns the first element that satisfies a condition if none then the default value.
13. **Last / LastOrDefault**: Returns the last element that satisfies a condition if none then or the default value.
14. **Single / SingleOrDefault**: Returns a single element that satisfies a condition if none then or the default value.
15. **ElementAt / ElementAtOrDefault**: Returns an element at a specified index if none then or the default value.
**Note**: the default prevents errors by returning null.
see [[LINQ Element Operators]] for samples.
##### Aggregation:
16. **Count**: Counts the number of elements in a sequence.
17. **Sum**: Calculates the sum of numeric elements.
18. **Min**: Finds the minimum element.
19. **Max**: Finds the maximum element.
20. **Average**: Computes the average of numeric elements.
21. **Aggregate**: Applies an accumulator function over a sequence.
see [[LINQ  Aggregation]] for samples.
##### Partitioning:
22. **Take**: Returns a specified number of elements from the beginning of a sequence.
23. **Skip**: Skips a specified number of elements from the beginning of a sequence.
see [[LINQ Partitioning]] for samples.
##### Quantifiers:
24. **Any**: Checks if any elements satisfy a condition.
25. **All**: Checks if all elements satisfy a condition.
26. **Contains**: Checks if a sequence contains a specified element.
see [[LINQ Quantifiers]] for samples.
##### Grouping:
27. **GroupBy**: Groups elements based on a common key.
28. **ToLookup**: Creates a lookup (dictionary-like) data structure based on a key.
see [[LINQ Grouping]] for samples.
##### Joining:
29. **Join**: Performs an inner join between two sequences.
30. **GroupJoin**: Performs a group join between two sequences.
31. **Zip**: Merges two sequences element-wise.
see [[LINQ Joining]] for samples.
##### Conversion:
32. **ToList**: Converts a sequence into a list.
33. **ToArray**: Converts a sequence into an array.
34. **ToDictionary**: Converts a sequence into a dictionary.
see [[LINQ Conversion]] for samples.
##### Set Operation (Boolean) Methods:
35. **SequenceEqual**: Compares two sequences for equality.
36. **Any / All**: Determine if any or all elements satisfy a condition.
see [[LINQ Set Operation (Boolean) Methods]] for samples.
##### Other:
37. **Reverse**: Reverses the order of elements in a sequence.
38. **Concat**: Concatenates two sequences.
39. **DefaultIfEmpty**: Provides a default value if a sequence is empty.
40. **Empty**: Creates an empty sequence.
41. **Repeat**: Repeats a sequence a specified number of times.
see [[LINQ Other Methods]] for samples.