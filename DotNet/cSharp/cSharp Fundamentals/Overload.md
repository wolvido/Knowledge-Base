---
keywords: multiple versions of a method or constructor
---
#cSharp 
constructor or methods with the same name but with different parameters or parameter lists. Basically a different version of a method to account for every possible use.
example:
```c#
public class Calculator
{

    public int Add(int a, int b)  // Method to add two integers
    {
        return a + b;
    }

    public int Add(int a, int b, int c)  // Method to add three integers
    {
        return a + b + c;
    }
    
    public double Add(double a, double b) // different version is also considered an overload
    {
        return a + b;
    }
}

class Program
{
    static void Main()
    {
        Calculator calc = new Calculator();

        int sum1 = calc.Add(5, 10); // Calls the first Add method (int version)
        int sum2 = calc.Add(3, 7, 2); // Calls the second Add method (int version)
        double sum3 = calc.Add(3.5, 2.7); // Calls the third Add method (double version)

        Console.WriteLine($"Sum 1: {sum1}");
        Console.WriteLine($"Sum 2: {sum2}");
        Console.WriteLine($"Sum 3: {sum3}");
    }
}
```
### Constructor overload sample:
```c#
public Person()// Default constructor with no parameters
{
	FirstName = "John";
	LastName = "Doe";
	Age = 30;
}

public Person(string firstName, string lastName)// Constructor overload with parameters for first name and last name
{
	FirstName = firstName;
	LastName = lastName;
	Age = 30; // Default age
}
```