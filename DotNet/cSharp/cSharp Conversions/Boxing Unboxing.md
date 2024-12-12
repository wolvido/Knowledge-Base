#cSharp 
converting value type to reference type and vice versa
# boxing:
```c#
int i = 42;
object obj = i; // Boxing: i is converted into an object
```
# unboxing:
```c#
int j = (int)obj; // Unboxing: obj is converted back to int
```

**NOTE:** 
as much as possible prevent boxing or unboxing because they are performance intensive. 
If you find yourself trying to use multiple data types, see [[Knowledge Base/DotNet/cSharp/cSharp Keywords and Additional Material/generic]] for an alternative.