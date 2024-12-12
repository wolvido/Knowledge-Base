#cSharp 
keywords:
	representative variable
	Representing data with readable values
	Representing Data with cleaner code
	custom representation
	substitute for data
	easier way to represent data
	enumeration

to make code readable. 
```c#
public enum Direction  
{  
	Up,  
	Down,  
	Left,  
	Right  
}  
```
##### Which is more readable? 
```changeDirection(1);```  
or
```changeDirection(Direction.Up);```
#### How Enums work
Enums are not groups of data, they are data grouped by enumeration, which means each value also has a number equivalent. For example:
```c#
public enum DaysOfTheWeek
{
	sun,
	mon,
	tue,
	wed,
	thu,
	fri,
	sat
}
```
So, all these values have number equivalents starting from sun = 1 to sat = 7.
#### Enums as limited choice data types
That's not the only us of enums, you can use enums to make your data type consistent and safe. For example:
```c#
public enum Gender { Male, Female, Other }

public class Person {
	public string Name { get; set; } 
	public Gender Gender { get; set; } 
}
```
This prevents string gender, forces the consumer to use only the limited options.
To use the data, simply convert to string, or cast to int.
```c#
Gender gender = Gender.Other; 

// Get the name of the enum value 
string genderName = gender.ToString(); // "Other" 

// Get the underlying integer value of the enum 
int genderValue = (int)gender; // 3 
```