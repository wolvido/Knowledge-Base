---
keywords: |-
  combining words
  	# What is it called when you inject variable in a string  	# should i use concatenation or interpolation  	# variable and string  	# variable + string  	# adding variable to string
---
concatenation:
```c#
var string1 = "Hello";  
var string2 = "world";  
var result = string1 + " " + string2;
```
interpolation:
```c#
var name = "Alice";  
var age = 25;  
var result = $"My name is {name} and I am {age} years old.";
```
dont forget the $ when interpolating in c#, or any equivalent in other languages.