>[!info]-  Reminder
>Server side scripting should only focus on the presentation logic. Business logic should always be handled by the back. see [[Business Logic vs Presentation Logic]]

### Basic Math
```c#
<div>
	@(10+50-20*30/40)
</div>
```
### If else:
```c#
@if(condition)
{
	//C# or html code
}
else
{
	//C# or html code
}
```
### switch:
```c#
@switch (variable)
{
	case value1: codeHere; break;
	case value2: codeHere; break;
	default: codeHere; break;
}
```
### foreach:
```c#
@foreach (var i in collection)
{
	//codeHere
}
```
>[!note]
>foreach also repeats any html tags inside it with a variable, same goes with for loop and any kind of loop
### for:
```c#
@for (int i = 0; i < 5; i++)
{
	//codeHere
}
```
### Local Functions
```c#
@{
	ReturnType MethodName(parameters)
	{
		//codeHere
	}
}
```
#### Inline Razor
```c#
@for (int i = 0; i < 4; i++)
{
	<div class="number-value">
	    @{
	        string value;
	        if (i == 3){
	            value = "cash";
	        }
	        else{
	            value = i.ToString();
	        }
	    }
	    @value
	</div>
}
```

### Html.Raw()
will read the text as raw code instead of just string.
```c#
@Html.Raw("<script>console.log()</script>")
```
the string version will be considered real raw code and executed.
