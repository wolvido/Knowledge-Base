---
keywords: |-
  sort a collection of objects
  sort objects
  compare objects
---
An interface that creates the contract CompareTo. 
```c#
public interface IComparable<in T>
{
    int CompareTo(T? other);
}
```
It is applied to custom classes where you need to compare its custom objects. 
If youre confused about the question mark, see [[Nullable Type]]. If youre confused about interface see [[Interface]]. If youre confused about **in** see [[Interface Generic Covariance Contravariance]].
###### Sample:
```c#
public class Person : IComparable<Person>
{
    public string Name { get; set; }
    public int Age { get; set; }

    // Implementing IComparable<T> where T is Person
    public int CompareTo(Person other)
    {
        // Custom comparison logic without using CompareTo or built-in comparisons
        if (this.Age < other.Age)
        {
            return -1; // This instance is "less" than the other instance
        }
        else if (this.Age > other.Age)
        {
            return 1; // This instance is "greater" than the other instance
        }
        else
        {
            return 0; // equal returns 0
        }
    }
}

public class Program
{
    public static void Main()
    {
        Person person1 = new Person { Name = "Alice", Age = 30 };
        Person person2 = new Person { Name = "Bob", Age = 25 };

        int result = person1.CompareTo(person2);

        if (result < 0)
        {
            Console.WriteLine($"{person1.Name} is younger than {person2.Name}");
        }
        else if (result > 0)
        {
            Console.WriteLine($"{person1.Name} is older than {person2.Name}");
        }
        else
        {
            Console.WriteLine($"{person1.Name} and {person2.Name} are the same age");
        }
    }
}
//note this is a fundamental example, see below for something better.
```
##### .Net has built in `CompareTo` for every data types, In general all of them implement `CompareTo`:
![[Standard comparison convention]]
**NOTE:** these are the 3 standard convention when implementing a `CompareTo` . Built in like int, double, or string has their own Implementation of CompareTo following the same rules, see example below if you dont understand.
###### You can also use the built in `CompareTo` of other types, sample:
```c#
public class Person : IComparable<Person>
{
    public string Name { get; set; }
    public int Age { get; set; }
    
    // Implementing IComparable<T> where T is Person
    public int CompareTo(Person other)
    {
	    //using the CompareTo of int type, since Age is int, essentially functions the same.
        return this.Age.CompareTo(other.Age); 
    }
}

public class Program
{
    public static void Main()
    {
        Person person1 = new Person { Name = "Alice", Age = 30 };
        Person person2 = new Person { Name = "Bob", Age = 25 };
        
        int result = person1.CompareTo(person2);
        
        if (result < 0)
        {
            Console.WriteLine($"{person1.Name} is younger than {person2.Name}");
        }
        else if (result > 0)
        {
            Console.WriteLine($"{person1.Name} is older than {person2.Name}");
        }
        else
        {
            Console.WriteLine($"{person1.Name} and {person2.Name} are the same age");
        }
    }
}
```



