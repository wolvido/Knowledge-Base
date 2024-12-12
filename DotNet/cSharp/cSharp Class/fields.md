#cSharp 
syntax:
```c#
[modifiers] type fieldName
```
for more info on modifiers go to [[Modifiers]]

ex: 
```c#
public int myPublicField; // Public field of type int  
private string myPrivateField; // Private field of type string 
protected static double myStaticField; // Protected static field of type double  
private readonly int myReadOnlyField; // Private readonly field of type int  
public const string MY_CONSTANT = "Hello"; // Public constant field of type string
```
**Note:**
Do not expose fields, properties should be exposed. If you just need a glorified public field use an auto property instead. see:[[properties]]. When in doubt, just use the most easy to understand.

>[!question] Why are fields needed?
>Well, What are you suppose to use? Your gonna create variables to manipulate data anyway, that's what fields are.

naming convention:  
-mosh uses \_camelCase for private fields, pascal for public fields/auto properties  
-for parameters he uses camelCase  
-Everything else he uses PascalCase