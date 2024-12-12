---
Keywords: |-
  # c# create index in a class  	
  # c# cookie class  	
  # c# collection class  	
  # c# dictionary class  	
  # c# class that stores collection  	
  # cSharp create index in a class  	
  # cSharp cookie class  	
  # charp collection class  	
  # charp dictionary class  	
  # charp class that stores collection  	
  # access element in a collection class  	
  # indexer class	
  # easier way to create a class that stores a collection  	
  # indexers  	
  # a way to create a class that can be an indexer  	
  # a way to create a class that can act as an indexer 
  class list
---
#cSharp 
sample dictionary style:
```cSharp
public class HttpCookie  
{  
	private readonly Dictionary<int, string> _dictionary = new();  
	  
	public string this[int key]  
	{  
		get { return _dictionary[key]; }  
		set { _dictionary[key] = value; }  
	}  
}
```
how to use:
```cSharp
HttpCookie cookie = new HttpCookie();  
cookie[1] = "test";  
cookie[2] = "test2";  
Console.Write(cookie[2]); //output "test2"
```
Note: Use a dictionary if you want to look up data using a key, like the example above. Use a list if you want to look up using an index. 
Example of a list indexer:
```cSharp
public class IndexedList  
{  
	private readonly List<int> myList = new();  
	  
	public int this[int index]  
	{  
		get { return myList[index]; }  
		set { myList.Add(value); }  
	}  
}
```
