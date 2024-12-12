#cSharp 
Delegate built-ins are nothing special, there basically just delegates already made with their own return types and parameters. They are used instead of a custom delegate because developers already know how what their return types are or their parameters etc..

in simple terms:
- **Action** = some method that just does something but returns no output
- **Func** = some method that takes some parameters, computes something and returns a result
- **Comparison** = some method that compares two objects of the same type and returns an int to indicate order
- **Converter** = transforms Obj A into equivalent Obj B
- **EventHandler** = response/handler to an event raised by some object given some input in the form of an event argument
- **Predicate** = evaluate input object against some criteria and return pass/fail status as bool
##### **1. Action:**
```c#
class Calculator
{
    private Action<string> logAction; // Action delegate for logging
    
    public Calculator(Action<string> logAction)
    {
        _logAction = logAction;
    }
    
    public int Add(int a, int b)
    {
        int result = a + b;
        
        _logAction($"Adding {a} and {b} equals {result}"); // Log the operation and result using the provided Action
        
        return result;
    }
    
    public int Subtract(int a, int b)
    {
        int result = a - b;
        
        _logAction($"Subtracting {b} from {a} equals {result}"); // Log the operation and result using the provided Action
        
        return result;
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Create a Calculator instance with an Action for logging
        Calculator calculator = new Calculator(Console.WriteLine); //inject Console.WriteLine for the Action
        
        // Perform some arithmetic operations and log the results
        int sum = calculator.Add(5, 3); //output: Adding 5 and 3 equals 8
        int difference = calculator.Subtract(10, 4); //output: Subtracting 4 from 10 equals 6
    }
}
//since its a calculator class, its ok to have built in arithmetic methods instead of making it extensible
```
###### simpler non class example:
```c#
using System;

class Program
{
    static void PrintHello()
    {
        Console.WriteLine("Hello, world!");
    }
    
    static void PrintGoodbye()
    {
        Console.WriteLine("Goodbye, world!");
    }
    
    static void PrintNumber(int num)
    {
        Console.WriteLine($"The number is: {num}");
    }
    
    static void Main()
    {
        Action actionPrintHello = PrintHello;
        actionPrintHello(); // Hello, world!
        
        Action actionPrintGoodbye = PrintGoodbye;
        actionPrintGoodbye(); // Goodbye, world!
        
        Action<int> actionPrintNumber = PrintNumber;
        for (int i = 1; i <= 5; i++)
        {
            actionPrintNumber(i); //"The number is: {num}"
        }
    }
}
```
###### Action is basically:
```c#
//just a shorter syntactic sugar of this
public delegate void Action < in P > (P obj);
//can also be:
public delegate void Action < in P1, in P2 > (P1 arg1, P2 arg2);
```
if you're confused about `in`, see [[Interface Generic Covariance Contravariance]].

`Action` primarily used when you want to represent and invoke a method or operation that takes parameters but does not return a value (returns `void`) like:
1. **Callback Functions:** You can use `Action` to define callback functions or event handlers that perform some action when a specific event occurs. For example, handling button clicks in a user interface.
2. **Asynchronous Programming:** In asynchronous programming, you might use `Action` to represent a method to execute upon the completion of an asynchronous operation.
3. **Logging and Side Effects:** When you need to perform logging or other side effects within a method but don't need to return any value, you can use an `Action` to encapsulate the side effect.
4. **Action for each:** Can be used in a for each loop to set an action for each.

##### **2. Func:**
Func is a delegate written in the system as:
```c#
public delegate TResult Func<in T,out TResult>(T arg);
//can also be:
public delegate TResult Func<in T1, in T2, out TResult>(T1 arg, T2 arg);
```
- `TResult` is the output type.
- the T or T1, T2 are the input types.
- T args are the normal parameters.
###### simple sample:
```c#
class Program 
{
	// Method
	public static int mymethod(int s, int d, int f, int g)
	{
		return s * d * f * g;
	}
	
	// Main method
	static public void Main()
	{
		// Here, Func delegate contains the four parameters of int type one result parameter of int type
		Func<int, int, int, int, int> val = mymethod;
		Console.WriteLine(val(10, 100, 1000, 1));
	}
}
```
If in case youre confused about feeding lambda to a func parameter, see [[Lambda]] at the bottome there's notes.
##### **3. Comparison:**
Syntax:
```c#
public delegate int Comparison<in T>(T x, T y);
```
- `T` is the input type
- `T x` The first object to compare.
- `T y` The second object to compare.
Rules:
- if x is less than y, return -1 or lesser
- if x is equal to y,  return 0
- if x is greater than y, return 1 or greater
- valid sample:
```c#
int CompareIntegers(int x, int y)
{
    if (x < y)
        return -1;
    else if (x > y)
        return 1;
    else
        return 0;
}
```

Code sample:
```c#
class Product
{
    public string Name { get; set; }
    public decimal Price { get; set; }
}
 
class Program
{
    // Define a separate method for the custom comparison logic
    static int CompareByPrice(Product product1, Product product2)
    {
        if (product1.Price < product2.Price)
        {
            return -1;  // product1 is younger, so it comes before product2
        }
        if (product1.Price > product2.Price)
        {
            return 1;   // product1 is older, so it comes after product2
        }
        return 0;   // product1 and product2 have the same Price
    }
 
    static void Main()
    {
        // Create a list of Product objects
        List<Product> products = new List<Product>
        {
            new Product { Name = "Laptop", Price = 800.00M },
            new Product { Name = "Smartphone", Price = 500.00M },
            new Product { Name = "Tablet", Price = 300.00M }
        };
 
        // Define a Comparison<Product> delegate explicitly
        Comparison<Product> priceComparison = CompareByPrice;
 
        // Use the Comparison delegate to sort the list by price
        products.Sort(priceComparison);
 
        // Print the sorted list
        foreach (var product in products)
        {
            Console.WriteLine($"Product: {product.Name}, Price: {product.Price:C}");
        }
    }
}
```
if youre confused about the .Sort see [[List]] sorting Sorting and Reversing section.

**I think by this point you already know how built in delegates work, I'm just going to add the syntax**
##### **3. Converter:**
syntax:
```c#
public delegate TOutput Converter<in TInput,out TOutput>(TInput input);
```
- TInput - The type of object that is to be converted.
- TOutput - The type the input object is to be converted to.
- TInput input - normal parameter, the object to convert.
- TOutput - the output/return modifier.
##### **4. EventHandler:**
syntax:
```c#
public delegate void EventHandler(object? sender, EventArgs e);
```
- sender - source of the event
- e - any additional data to send, by default `EventArgs.Empty` when no additional data is needed.
##### **5. Predicate:**
syntax:
```c#
public delegate bool Predicate<in T>(T obj);
```
- T - input type
- T obj - The object to compare against the criteria defined within the method represented by this delegate.
- bool - `true` if `obj` meets the criteria defined within the method represented by this delegate; otherwise, `false`.