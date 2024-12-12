#cSharp 
keywords:
	way to manipulate string
Insert:
```c#
StringBuilder sb = new StringBuilder("Hello World!");  
sb.Insert(5, " Awesome");  
string result = sb.ToString();  
Console.WriteLine(result);
```
Append:
```c#
StringBuilder sb = new StringBuilder();  
sb.Append("Hello");  
sb.Append(" World!");  
Console.WriteLine(sb.ToString());
```
Replace:
```c#
StringBuilder sb = new StringBuilder("Hello World!");  
sb.Replace("World", "Universe");  
Console.WriteLine(sb.ToString());
```
Remove:
```c#
StringBuilder sb = new StringBuilder("Hello World!");  
sb.Remove(5, 5); // Removes " World"
```
Clear:
```c#
StringBuilder sb = new StringBuilder("Hello World!");  
sb.Clear(); // Clears the StringBuilder, making it empty
```
ToString:
```c#
StringBuilder sb = new StringBuilder("Hello World!");  
string result = sb.ToString();
```