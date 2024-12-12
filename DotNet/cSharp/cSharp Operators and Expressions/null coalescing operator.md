---
keywords: double question mark
---
#cSharp 
**not to be confused with [[null conditional operator]] or [[Nullable Type]].**
syntax:
```c#
result = expression1 ?? expression2;
```
- If `expression1` is not null, the result is `expression1`.
- If `expression1` is null, the result is `expression2`.
sample:
```c#
int? nullableValue = null;
int result = nullableValue ?? 10; // If nullableValue is null, result will be 10
```
