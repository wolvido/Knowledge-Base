Exactly the same as [[Action Filter]] but instead of filtering the action method, it filters the view/IActionResult to be returned by the action method, aka the [[HTTP Response]].
![[Screenshot 2024-03-06 at 15-54-42 Asp.Net Core 8 (.NET 8) True Ultimate Guide.png]]
#### What's the point of filtering the IActionResult/View?
Modify or inspect the result (response) of an action method before it's sent to the client.
- It can short circuit the IActionResult and return a different IActionResult. see: [[Filter Short Circuit]].
- Format the IActionResult as necessary; modify the [[HTTP Response]].
###### In the real world, it is rarely used, it is mostly used when you need to edit anything in the HTTP Response.
# How-To:
The creation works the same as [[Action Filter]], the difference is in method name, the interface, and the folder location.
- First, in your Filters folder, create the folder "ResultFilters".

Syntax:
```c#
public class SampleResultFilter : IResultFilter
{
	public void OnResultExecuting(ResultExecutingContext context)
	{
		//code that will execute before the response is sent
	}
	public void OnResultExecuted(ResultExecutingContext context)
	{
		//code that will execute after the response is sent
	}
}
```
This is the non-async version, don't forget, you can also [[Asynchronous Filter]].
###### Also, don't forget, you can always access or modify anything in the **`ActionExecutedContext`** for whatever logic you need.

###### To short circuit you use context.Result:
```c#
public class SampleResultFilter : IResultFilter
{
	public void OnResultExecuting(ActionExecutingContext context)
	{
		//code that will execute before the response is sent
		if(...)
		{
			return context.Result = //whatever you need to happen to the result
			
			//sample:
			return context.Result = new NotFoundResult(); //404 not found
		}
	}
}
```



