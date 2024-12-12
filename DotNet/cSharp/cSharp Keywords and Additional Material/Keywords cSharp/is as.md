---
keywords: |-
  is
  as
  how to check if casting is valid
  how to check if upcasting is valid
  how to check if downcasting is valid
---
#cSharp 
used in downcasting to check if casting is valid.
see [[casting]] for more info.
# is:
```c#
if (obj is Car) //if object is allowed to cast
{
	Car car = (car) obj;
}
else
{
	//not possible to cast
}
```
# as:
```c#
Car car = obj as Car: //will return null if obj cannot be casted to car
if (car != null) 
{
	//cast success
}
```