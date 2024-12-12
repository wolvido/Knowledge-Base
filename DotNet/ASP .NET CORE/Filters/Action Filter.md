It is filter code that will execute before and after an action method.
As soon as the route knows which action to take, **`OnActionExecuting`** will execute before execution of the action method, and after the action method has executed, **`OnActionExecuted`** executes.
![[Pasted image 20240229161112.png]]
#### What's the point?
Well... its a filter, so depending what you need filtered you can:
**`OnActionExecuting`**:
- access the action method parameters, read them and do necessary manipulations.
- also validate the parameters.
- prevent the action method from executing if the user enters invalid parameters and return a different Action Result. [[Filter Short Circuit]]
**`OnActionExecuted`**:
- manipulate the view data, maybe add new data or remove.
- manipulate the action method return.
- can throw exceptions.
**IMPORTANT:** It does not and should not filter the result of the action method, it should only filter the processes of the action method. Filtering the result is the job of [[Result Filter]].
###### **`OnActionExecuting`** and **`OnActionExecuted`** is written in a single class called Action Filter class
# How-To create an Action Filter Class:
- First in you main project, create the folder "Filters". This folder will contain all types of filters.
- Then, create a sub folder called "ActionFilters"
- Create a new item on the folder, name it appropriately depending on its purpose, for example if your Index Action method returns a list of **`Person`** type, and you need to filter the list, name it **`PersonsListActionFilter`**.  Name it by its purpose.
- Then inherit from **`IActionFilter`**. **`IActionFilter`** has the two method contracts **`OnActionExecuted`** and **`OnActionExecuting`**, implement it on your Action Filter.
Syntax:
```c#
public class PersonsListActionFilter : IActionFilter
{
	public void OnActionExecuting(ActionExecutingContext context)
	{
		//code that will execute before the action method
	}
	public void OnActionExecuted(ActionExecutedContext context)
	{
		//code that will execute after the action method
	}
}
```
##### **`ActionExecutingContext`** is the context of the executing action method.
Essentially, here you can access the action arguments, http context, controller, route data, all the properties you need to access for the action method executing.
This is also where you can access the view bag/view data, through accessing the controller. You'll see everything in intellisense.
This is what you will use to set up data for whatever logic you need.
#### Applying the filter
To attach the action filter to the action method:
```c#
[TypeFilter(typeof(PersonsListActionFilter))]
public async Task<IActionResult> Index()
{
	//codes...
}
```
#### Validation in ActionFilter
One of the common uses of an action filter is for validation.
Lets say you have an index action method that accepts the parameter `searchBy`. 
It will provide what to search the person by whether its the name, email, gender etc., **`searchBy`** will provide what to search the person by, and `searchString` will provide the what the name, email, gender etc..
```c#
public async Task<IActionResult> Index(string searchBy, string? searchString)
{
	//will return a Persons list
}
```
Now, we need to validate that `searchBy` is correct.
```c#
public class PersonsListActionFilter : IActionFilter
{
	public void OnActionExecuted(ActionExecutedContext context)
	{
		//code that will execute after the action method
		//add whatever you need here, maybe modify the return, or logging, or error handling etc..
	}
	public void OnActionExecuting(ActionExecutingContext context)
	{
		//everything is in the context, the arguments of the action method is in the dictionary called ActionArguments
		if (context.ActionArguments.ContainsKey("searchBy")) //if searchBy exists in ActionArguments
		{
			string? searchBy = Convert.ToString(context.ActionArguments["searchBy"]); 
				//get the value of searchBy parameter from ActionArguments
			
		    //if searchBy exist
		    if (!string.IsNullOrEmpty(searchBy))
		    {
			    //get the values that you can search it by
				var searchByOptions = new List<string>() 
				{ 
					nameof(Person.PersonName),
					nameof(Person.Email),
					nameof(Person.DateOfBirth),
					nameof(Person.Gender),
					nameof(Person.CountryID),
					nameof(Person.Address)
				};
				
				//then check if searchBy matches with atleast one searchByOptions
				if (searchByOptions.Any(temp => temp == searchBy) == false) //this is a linq code, dont get confused
				{
					//if it does not see any match, it means the searchBy parameter was wrong somehow
					//therefore we reset the searchBy value
					context.ActionArguments["searchBy"] = nameof(Person.PersonName); //reset to name
					
					//maybe add some logging here..
				}
			}
		}
	}
}
```


>[!warning]
>**`context.ActionArguments`** cannot be accessed in **`OnActionExecuted`**, If you really need to, there is a way involving using **`HttpContext.Items`**.

>[!info] disclaimer
>This sample is one of harshas stupid very specific sample, that is too specific to be used in any other way. 
>Just use it as a reference to let you know one sample of its uses.
>Either way you can extrapolate how to validate using Filters. Just add the logic in inside the `OnActionExecuting` or `OnActionExecuted`.
#### ViewData in Action Filter
How to access view data in action filter?
To access the view data in the filter, you need to cast `context.Controller` into the controller type first.
```c#
public class MyActionFilter : IActionFilter
{
	public void OnActionExecuted(ActionExecutedContext context)
	{
		//type casting
		SampleController sampleController = (SampleController)context.Controller;
		
		//getting ViewData
		var data = sampleController.ViewData["whatever"];
		//setting ViewData
		sampleController.ViewData["whatever"]; = "whatever";
		
		//dont forget you need to validate this, especially if it the value does not exist
	}
}
```
# What Next?
- learn how to parameters/argument to an action filter [[Filter with arguments]].
- how to filter all of the action methods instead of just the one action method? [[Class Level Filter]]