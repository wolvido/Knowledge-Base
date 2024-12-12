#cSharp 

```c#
class Address
{
    public string Street { get; set; }
    public string City { get; set; }
    public string PostalCode { get; set; }

    public Address(string street, string city, string postalCode)
    {
        Street = street;
        City = city;
        PostalCode = postalCode;
    }
}

class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public Address HomeAddress { get; set; }

    public Person(string name, int age, Address address)
    {
        Name = name;
        Age = age;
        HomeAddress = address;
    }
}

class Program
{
    static void Main()
    {
        // Create an Address object
        Address address = new Address("123 Main St", "Cityville", "12345");

        // Create a Person object with the Address object as a parameter
        Person person = new Person("John Doe", 30, address);

        // Accessing properties of the Person and Address objects
        Console.WriteLine($"Name: {person.Name}");
        Console.WriteLine($"Age: {person.Age}");
        Console.WriteLine($"Address: {person.HomeAddress.Street}, {person.HomeAddress.City}, {person.HomeAddress.PostalCode}");
    }
}
```