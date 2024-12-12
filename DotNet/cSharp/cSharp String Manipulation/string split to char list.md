#cSharp 
keywords:
	-string split
	-string split to list

Syntax:
```c#
// To split a string use 'Split()', you can choose where to split  
string text = "Hello World!"  
string[] textSplit = text.Split(" ");  
// Output:  ["Hello", "World!"]
```
Note: split returns an array not a list, to convert into list use:
```c#
text.Split(" ").ToList();
```
to split for each character of a string to a list:
```c#
string data = "ABCDEFGHIJ1fFJKAL";  
List<char> datalist = new List<char>();  
datalist.AddRange(data);
```
to split for each character of a string to an array:
```c#
String.ToCharArray()
```
Note: Array is not recommended for manipulation