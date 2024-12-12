---
keywords: Question mark in the middle
---
#cSharp 
**not to be confused with [[Nullable Type]] or [[null coalescing operator]].**
```c#
var result = object?.property
```
- `obj` is the object you want to access.
- `Property` is the property you want to access on `obj`.

With the null conditional operator, if `obj` is null, `result` will be set to null, and no exception will be thrown. If `obj` is not null, `result` will be set to the value of `obj.Property`.
sample:
```c#
// For both of these examples, if 'p' is null, 'nameResult' and 'ageResult' will be null 
// (as opposed to throwing an error)
string nameResult = p?.FirstName;
string ageResult = p?.Age;
```
on if else sample:
```c#
string result = someObject?.ToString();

//is short for

string result;
if (someObject != null)
{
    result = someObject.ToString();
}
else
{
    result = null;
}
```