#cSharp 
[[multi dimension arrays]]

Array is a collection of the same data type
Array in c#: 
``` c#
int[ ] numbers = new int[3] {1,2,3};  
```
can be shorthand for:
```c#
int[ ] numbers = {1,2,3};  
```
can also be:
```c#
var numbers = new[] { 1, 2, 3, 4 };
```
note: can be any data type.

array can be initialized by: 
```c#
int[ ] numbers =new int[3];
```
Array index in C#:
```c#
int[ ] numbers = {1,2,3};  
//numbers[0] would be equal to 1.
```
### c# array methods:
Length: It returns the total number of elements in the array.
```c#
int[] numbers = { 1, 2, 3, 4, 5 };  
int length = numbers.Length; // length is 5
```
IndexOf: It searches for the specified value and returns the index of the first occurrence in the array.
```c#
int[] numbers = { 1, 2, 3, 4, 5 };  
int index = Array.IndexOf(numbers, 3); // index is 2
```
Contains: It checks whether the array contains a specific value and returns a Boolean value indicating the result.
```c#
int[] numbers = { 1, 2, 3, 4, 5 };  
bool containsThree = numbers.Contains(3); // containsThree is true
```
Sort: It sorts the elements in the array in ascending order.
```c#
int[] numbers = { 5, 2, 1, 4, 3 };  
Array.Sort(numbers); // numbers is { 1, 2, 3, 4, 5 }
```
Reverse: It reverses the order of the elements in the array.
```c#
int[] numbers = { 1, 2, 3, 4, 5 };  
Array.Reverse(numbers); // numbers is { 5, 4, 3, 2, 1 }
```
Copy: It creates a shallow copy of the array or a specific range of elements.
```c#
int[] source = { 1, 2, 3, 4, 5 };  
int[] destination = new int[5];  
Array.Copy(source, destination, 5); // destination is { 1, 2, 3, 4, 5 }
```
Clear: It sets a range of elements in the array to their default values (0 for numeric types, null for reference types).
```c#
int[] numbers = { 1, 2, 3, 4, 5 };  
Array.Clear(numbers, 1, 3); // numbers is { 1, 0, 0, 0, 5 }
```
Resize: It changes the size of the array.
```c#
int[] numbers = { 1, 2, 3 };  
Array.Resize(ref numbers, 5); // numbers is { 1, 2, 3, 0, 0 }
```