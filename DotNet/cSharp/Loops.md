#cSharp 
CSharp Loops:
	[[in for loops why less than does not include equal]]

for loops:  
```c#
for(int i = 0; i < 3; i++)  
{  
	code  
}  
```
for each: 
```c#
foreach (var i in enumerable)  
{  
	code  
}  
```
Notes:  
	-Enumerable is anything is a list or an array nature. string is also enumerable.  
	-In for loop, the statement is executed before the iterator, this will result in for loop starting at the iterator.  
  
while loop:  
```c#
while (condition)  
{  
	code  
}  
```
example:  
```c#
while (i < 10)  
{  
	code  
	i++  
}  
```
do while:  
```c#
//works the same as while loop bot code runs first  
do  
{  
code  
} while (condition);  
```
Note:  
```c#
for (int i = 0; i <= 2; i++)  
{  
	Console.WriteLine(i);  
} 
``` 
is equal to:  
``` c#
var counter = 0;  
while (counter <= 2)  
{  
	Console.WriteLine(counter);  
	counter++;  
}
```
#### less than equals vs less than:
```c#
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

output
0
1
2
3
4
```
```c#
for (int i = 0; i <= 5; i++)
{
    Console.WriteLine(i);
}

output
0
1
2
3
4
5
```
**Remember: if greater than, then it goes on reverse**