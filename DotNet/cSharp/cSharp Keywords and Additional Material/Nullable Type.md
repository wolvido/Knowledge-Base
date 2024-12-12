---
keywords: |-
  Question mark after data Type
  type?
  type question mark
  type questionmark
---
#cSharp 
**not to be confused with [[null conditional operator]] or [[null coalescing operator]].**
Allows for a null type in any type.
example:
```c#
Nullable<int> test = null;
int test = null; //will throw an error
```
shorthand sugar:
``` c#
int? test = null;
```

also works for parameters, sample:
```c#
public void MyMethod(string? nullableString) //means nullableString can accept null or string
{
    if (nullableString != null)
    {
        // You can safely access methods and properties on nullableString here
        int length = nullableString.Length;
    }
    else
    {
        // nullableString is null
    }
}
```
**Note**:
You cannot cast a nullable type into a non nullable type.
sample:
```c#
DateTime? date = new DateTime(2014, 1, 1);
DateTime date2 = date; //will not build
```
in case, you can use:
```c#
DateTime? date = new DateTime(2014, 1, 1);
DateTime date2 = date.GetValueOrDefault(); //will return the default value of the type
```
the opposite will work of course:
```c#
DateTime date = new DateTime(2014, 1, 1);
DateTime? date2 = date; //will not build
```


