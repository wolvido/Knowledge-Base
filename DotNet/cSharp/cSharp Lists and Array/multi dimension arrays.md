#cSharp 
keywords: 
	-matrix arrays

-2d rectangular array syntax:
```c#
var matrix = new int[3, 5]  
{  
	{ 1, 2, 3, 4, 5 },  
	{ 6, 7, 8, 9, 10 },  
	{ 8, 9, 10, 11, 12 }  
};  
var element = matrix[1, 3]; //element = 9
//first value is row, second is column
```
-3d rectangular array:
```c#
var matrix3d = new int[2, 2, 2]  
{  
	{  
		{1, 2},  
		{3, 4}  
	},  
	{  
		{5, 6},  
		{7, 8}  
	}  
};  
  
var elem1 = matrix3d[0, 0, 0]; // returns 1  
var elem2 = matrix3d[0, 0, 1]; // returns 2  
var elem3 = matrix3d[0, 1, 0]; // returns 3  
var elem4 = matrix3d[0, 1, 1]; // returns 4  
var elem5 = matrix3d[1, 0, 0]; // returns 5  
var elem6 = matrix3d[1, 0, 1]; // returns 6  
var elem7 = matrix3d[1, 1, 0]; // returns 7  
var elem8 = matrix3d[1, 1, 1]; // returns 8
```
-4d rectangular array:
```c#
var matrix4d = new int[2, 2, 2, 2]  
{  
	{  
		{  
			{1, 2},  
			{3, 4}  
		},  
		{  
			{5, 6},  
			{7, 8}  
		}  
	},  
	{  
		{  
			{1, 2}, 
			{3, 4}  
		},  
		{  
			{5, 6},  
			{7, 8}  
		}  
	}  
};
var element = matrix4d[0, 1, 0, 1]; //returns 6
```
Note: the first parameter of a multidimensional array is the first container, the second container is the second parameter so on and so forth, until we reach the index of the innermost array. This goes on to dimension 5th, 6th, 7th etc..

Jagged Array syntax:
to initialize:
```c#
var jaggedArray = new int[3][ ];  
jaggedArray[0] = new int[] { 1, 2, 3 };  
jaggedArray[1] = new int[] { 4, 5 };  
jaggedArray[2] = new int[] { 6, 7, 8, 9 };
```
to access the data:
```c#
int value = jaggedArray[1][1]; //equals 5
```
Note the var is just sugar, the original way of initializing an array is type[ ] ex. int[ ] or string[ ].