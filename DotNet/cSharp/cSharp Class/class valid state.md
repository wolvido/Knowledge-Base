#cSharp 
Keywords: 
	# class must always be in a valid state

example:  
```cSharp
public class Person  
{  
	private string name;  
	private int age;  
	  
	public Person(string personName, int personAge)  
	{  
		// Validation checks to ensure a valid state  
		if (string.IsNullOrWhiteSpace(personName))  
	{  
		throw new ArgumentException("Name cannot be null or empty.", nameof(personName));  
	}  
	  
	if (personAge <= 0)  
	{  
		throw new ArgumentException("Age must be a positive integer.", nameof(personAge));  
	}  
	  
	// Assigning values to the fields  
	name = personName;  
	age = personAge;  
	}  
	  
	public void DisplayDetails()  
	{  
		Console.WriteLine($"Name: {name}, Age: {age}");  
	}  
}  
  
public class Program  
{  
	public static void Main()  
	{  
		try  
		{  
		// Creating a Person object with valid data  
		Person person1 = new Person("John Doe", 25);  
		person1.DisplayDetails(); // Output: Name: John Doe, Age: 25  
		  
		// Creating a Person object with invalid data  
		Person person2 = new Person("", -5); // Throws ArgumentException  
		}  
		catch (ArgumentException ex)  
		{  
			Console.WriteLine(ex.Message);  
		}  
	}  
}
```
