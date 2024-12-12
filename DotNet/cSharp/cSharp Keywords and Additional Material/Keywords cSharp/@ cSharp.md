#cSharp 
In C#, when you prefix a string literal with the "@" symbol, it indicates that the string is a verbatim string literal. Verbatim string literals are used to treat backslashes "" as ordinary characters rather than escape characters.
```c#
string filePath = @"C:\Users\Username\Documents\file.txt";
```
In this verbatim string literal, the backslashes are treated as regular characters, so you don't need to escape them with an additional backslash. Without the "@" symbol, you would have to write it like this:
```c#
string filePath = "C:\\Users\\Username\\Documents\\file.txt";
```