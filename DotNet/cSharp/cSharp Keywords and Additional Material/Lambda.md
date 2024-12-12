---
keywords: |-
  C# arrow
  cSharp arrow
---
#cSharp 

its basically js anonymous function
syntax:
```c#
(parameters) => expression
```
sample:
```c#
class Program
{
    static void Main()
    {
        // method to calculate the sum of two numbers
        int AddNumbers(int a, int b)
        {
            return a + b;
        }
        
        // the lambda version of AddNumbers method
        Func<int, int, int> add = (a, b) => a + b;
        
        int result = add(5, 7);
        Console.WriteLine("Result: " + result);
    }
}
```
see [[Delegate Built-ins]] func section if youre confused about func

##### A more complex  sample below.
==Non-lambda Vanilla version:==
```c#
//this is non lambda version
class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        List<int> evenNumbers = GetEvenNumbers(numbers);

        Console.WriteLine("Even Numbers:");
        foreach (int number in evenNumbers)
        {
            Console.WriteLine(number);
        }
    }

    static List<int> GetEvenNumbers(List<int> numbers)
    {
        List<int> evenNumbers = new List<int>();
        foreach (int number in numbers)
        {
            if (number % 2 == 0)
            {
                evenNumbers.Add(number);
            }
        }
        return evenNumbers;
    }
}
```

lambda version of the code:
```c#
class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
        
        List<int> evenNumbers = numbers
	        .Where(number => number % 2 == 0) // where accepts func, it returns IEnumerable
	        .ToList(); //so we convert it back to list
            
        Console.WriteLine("Even Numbers:");
        foreach (int number in evenNumbers)
        {
            Console.WriteLine(number);
        }
    }
}
```
it is much much shorter.

**Notes:**
- if you're confused on what `number` is in the lambda, `number` is the parameter.
- If youre confused on why were feeding lambda on a delegate like func, thats because delegate is a data type that stores method, and the  delegate parameter is a data type so you feed it an object of that data type, which is a method.