#cSharp 
syntax:
```c#
var numbers = new List<int>();  
var numbers = new List<int>() {1, 2, 3, 4};
```
without var:
```c#
List<int> numbers = new List<int>();
```
indexing:
```c#
var firstElement = myList[0]; // Access the first element (42)
var secondElement = myList[1]; // Access the second element (24)
var thirdElement = myList[2];  // Access the third element (12)
```

list methods:
list have so many methods, these are the commonly used:
#### Adding and Removing Elements:
Add: Adds an element to the end of the list.  
AddRange: Adds the elements of a collection to the end of the list.  
Insert: Inserts an element at the specified index.  
InsertRange: Inserts the elements of a collection at the specified index.  
Remove: Removes the first occurrence of a specific element.  
RemoveAll: Removes all elements that match the specified condition.  
RemoveAt: Removes the element at the specified index.  
RemoveRange: Removes a range of elements, starting from the specified index.  
Clear: Removes all elements from the list.
#### Accessing and Finding Elements:
list`[int index]`: Gets or sets the element at the specified index.  
Find: Finds the first element that matches the specified condition.  
FindAll: Finds all elements that match the specified condition.  
FindIndex: Finds the index of the first element that matches the specified condition.  
FindLast: Finds the last element that matches the specified condition.  
FindLastIndex: Finds the index of the last element that matches the specified condition.  
Contains: Determines whether the list contains a specific element.
Exists: Determines whether an element that matches the specified condition exists in the list.  
IndexOf: Returns the index of the first occurrence of a specific element.  
LastIndexOf: Returns the index of the last occurrence of a specific element.  
GetRange: return a values based on index range.
#### Sorting and Reversing:
Sort: Sorts the elements in the list in ascending order.  
``Sort(Comparison<T> comparison)``: Sorts the elements using the specified comparison.  
``Sort(IComparer<T> comparer)``: Sorts the elements using the specified comparer.  
``Sort(int index, int count, IComparer<T> comparer)``: Sorts a range of elements using the specified comparer.  
Reverse: Reverses the order of the elements in the list.
#### Enumeration and Iteration:
ForEach: Performs a specified action on each element in the list.  
GetEnumerator: Returns an enumerator that iterates through the list.
#### Copying and Converting:
ToArray: Copies the elements of the list to a new array.  
CopyTo: Copies the entire list or a range of elements to an existing array.  
ConvertAll: Converts each element to another type using the specified converter.
#### Other Methods:
Count: Gets the number of elements in the list.  
Capacity: Gets or sets the total number of elements the list can hold without resizing.  
TrimExcess: Sets the capacity to the actual number of elements in the list, if it is below a certain threshold.
Sum: sum all numbers in the list.

the rest of them can be found here:  
for net 7  
[https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-7.0](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-7.0)