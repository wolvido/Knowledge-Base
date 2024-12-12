keywords:
	key:value

for structuring data
basically a key is a representation of the value  
  
example:  
book1: harry potter  
book2: bible

to create a dictionary
```c#
IDictionary<int, string> numberNames = new Dictionary<int, string>();
numberNames.Add(1,"One"); //adding a key/value using the Add() method
numberNames.Add(2,"Two");
numberNames.Add(3,"Three");
```