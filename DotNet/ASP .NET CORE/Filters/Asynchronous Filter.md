In case you want to call async methods, like repo methods or any other async methods. You might want to Asynchronize the filter methods.
If you don't need to call any async methods, this is not necessary.
# How-To:
- By inheriting and implementing **`IAsyncActionFilter`** instead of just **`IActionFilter`**; all else equal.
	- For [[Result Filter]] you will use **`IAsyncResultFilter`**.
	- For [[Resource Filter]] you will use **`IAsyncResourceFilter`**.
	- For [[Authorization Filter]] use **`IAsyncAuthorizationFilter`**.
	- For [[Exception Filter]] the syntax is different, see its note.
	- For [[Filter Attribute]]s, you will just override the async methods, see its note.
- **`OnActionExecuting`** and **`OnActionExecuted`** will also be converted to only one method **`OnActionExecutingAsync`**.
Syntax:
```c#
public class SampleFilter : IAsyncActionFilter //IActionFilter is replaced
{
	public async Task OnActionExecutingAsync(ActionExecutingContext context, ActionExecutionDelegate next)
	{
		//instead of `OnActionExecuting` and `OnActionExecuted`, we will write the before and after logic using next()- 
		//just like in middleware where you pass to the next.
		
		//before action method filter logic
		//here you put the logic where you would put in on OnActionExecuting if not async.
		
		await next(); //Next passes it to the next filter or action method, anything below here will be run later
		
		//after action method filter logic
		//here you put the logic where you would put in on OnActionExecuted
	}
}
```
**`ActionExecutingContext`** is the context of the executing action method, essentially, here you can access the http context, controller, action arguments, route data, all the properties you need to access for the action method executing.

