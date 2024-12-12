#cSharp 

- **GroupBy**: Groups elements based on a common key.
- **ToLookup**: Creates a lookup (dictionary-like) data structure based on a key.

```c#
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

List<Person> people = new List<Person>
{
    new Person { Name = "Alice", Age = 30 },
    new Person { Name = "Bob", Age = 25 },
    new Person { Name = "Charlie", Age = 30 },
    new Person { Name = "David", Age = 25 },
};

// GroupBy: Groups elements based on a common key
var groupedByAge = people.GroupBy(person => person.Age);
Console.WriteLine("Grouped by Age:");
foreach (var group in groupedByAge)
{
    Console.WriteLine($"Age: {group.Key}");
    foreach (var person in group)
    {
        Console.WriteLine($"Name: {person.Name}");
    }
}

// ToLookup: Creates a lookup (dictionary-like) data structure based on a key
var lookupByAge = people.ToLookup(person => person.Age);
Console.WriteLine("Lookup by Age:");
foreach (var group in lookupByAge[30])
{
    Console.WriteLine($"Name: {group.Name}");
}
```