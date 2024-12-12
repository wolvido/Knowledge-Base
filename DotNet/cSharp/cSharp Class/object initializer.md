#cSharp 
keywords:
	-C# object initialize  
	-C# how to easily add data to class  
	-C# add data to class after initializing  
	-C# initializing using collection
	-C# easier intialization
	-Csharp object initialize  
	-Csharp how to easily add data to class  
	-Csharp add data to class after initializing  
	-Csharp initializing using collection
	-Csharp easier intialization

A syntactic sugar. An easier way to initialize many class data

ex:
instead of:
```c#
var person = new Person();  
person.FirstName = first;  
person.LastName = last;
```
you can use:
```c#
var person = new Person  
{  
	FirstName = first,  
	LastName = last  
};
```
or if you only want one data::
```c#
var person = new Person  
{  
	FirstName = first  
};
```
note: resharper automates this.
note: if you have many data fields with the same data type, you could use params instead of object initialization.