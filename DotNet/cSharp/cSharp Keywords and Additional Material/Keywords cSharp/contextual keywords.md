Here's an example to illustrate this concept:

In C#, the keyword `yield` has a special meaning when used in a context that defines an iterator block. For example:

```c#
// An iterator block using 'yield' keyword
public IEnumerable<int> GetNumbers()
{
    yield return 1;
    yield return 2;
    yield return 3;
}
```
In this context, `yield` is a contextual keyword with a specific meaning related to creating an iterator.

However, outside the context of an iterator block, `yield` can be used as a regular identifier:
```c#
// 'yield' used as a regular identifier
int yield = 10;
Console.WriteLine(yield); // Output: 10
```
In this example, `yield` is just a variable name and does not have any special meaning related to iterators.