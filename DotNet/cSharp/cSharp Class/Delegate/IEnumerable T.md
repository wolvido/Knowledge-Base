# `IEnumerable<T>`
It creates an enumerable collection that is type `T`.
Sample:
```c#
class Program
{
    static void Main()
    {
        foreach (var number in GetNumbers())
        {
            Console.WriteLine(number); //output is 1 2 3 4 5
        }
    }

    static IEnumerable<int> GetNumbers()
    {
        for (int i = 1; i <= 5; i++)
        {
            yield return i;
        }
    }
}
```
In the sample, `GetNumbers()` is a collection of integers from 1 to 5 as created by the for loop. 
#### What is yield?
as you have guessed from the sample, yield postpones the return and instead waits for the for loop to finish and add all iteration **`i`** into a collection.
The whole purpose of a yield is to add items in a list per result of an iterator.

>[!question] So its basically `List<T>`?
> No, `IEnumerable<T>` is an interface, so it describes behavior, list is an implementation of that behavior.
> see [[Interface]] for more explanation.
> see this also [c# - IEnumerable vs List - What to Use?](https://stackoverflow.com/questions/3628425/ienumerable-vs-list-what-to-use-how-do-they-work)