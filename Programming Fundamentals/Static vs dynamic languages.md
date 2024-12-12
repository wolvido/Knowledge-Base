Static typing is when the data type of the variable is known at compile time.

Dynamic typing is when the data type of the variable is determined at run time.

Java and C# is a statically typed language. JavaScript and python is a dynamically typed language.

static c#:
```c#
int number = 5;
```
dynamic python:
```python
number = 5;
```
In static typed like c# number variable will always be checked before compile time, and thus be prevented from having type related errors. In dynamic typed like python, number variable will execute and might cause an type error at runtime, but its advantage is an easier to write and more human friendly code.

Static:
Every type is checked before compilation or interpretation, even an unreachable else is checked.

Dynamic:
Types are checked at runtime, an unreachable else with a type error will not throw an error since the runtime doesn't check it.

see [[What is CLR, JIT, IL]]
see [[Compiled vs interpreted]]