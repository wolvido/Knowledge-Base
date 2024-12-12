#cSharp 
We can see the _difference_ when one (or both strings) is `null`:
```csharp
string s1 = null;
string s2 = "World";

Console.WriteLine(s1.CompareTo(s2)); //will throw an error
Console.WriteLine(string.Compare(s1,s2)); // -1, since null < "World"
```

of course they follow the same standard:
![[Standard comparison convention]]

**Also** ``Compare()`` is a static method, CompareTo is its own implementation following the contract of [[IComparable]].