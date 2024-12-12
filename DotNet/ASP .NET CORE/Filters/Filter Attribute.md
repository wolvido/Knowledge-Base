Apply Filters as a direct attribute instead of through **`TypeFilter`**.
It's usually not used since you cannot injected anything in a Filter Attribute.
If you really need to use this style, then it might be better to use [[IFilterFactory]], it allows injection.
>[!warning]
>You cannot inject anything in a Filter Attribute, that also includes the logger.
>Also, can only be used for Action Filter, Result Filter and, Exception Filter; skip this note otherwise.
###### For example:
Instead of this:
```c#
[TypeFilter(typeof(SampleActionFilter), Arguments = new object[] {Parameter1, Parameter2} )]
public async Task<IActionResult> Index()
{
	//codes...
}
```
You can just do this:
```c#
[SampleActionFilter(Parameter1, Parameter2)] //applied as its own attribute
public async Task<IActionResult> Index()
{
	//codes...
}
```
# How-To:
Instead creating a filter that inherits from **`IActionFilter`** or **`IResultFilter`** etc., or their async version.
You will instead inherit from **`ActionFilterAttribute`**, **`ResultFilterAttribute`**, and **`ExceptionFilterAttribute`**.
>[!info]-
>Notice, I only put those three filters, Harsha said those are the only Filter Attribute supported by .NET for now. Since they are the most commonly used.
#### Syntax:
the syntax is the same, just swap the interface:
```c#
//syntax for an action filter attribute
public class SampleActionFilter : ActionFilterAttribute
{
	public SampleActionFilter(type arg1, type arg2, ...)
	{
	}
	
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
Then you will implement it directly:
```c#
[SampleActionFilter(arg1, arg2, ...)]
public async Task<IActionResult> Index()
{
	//codes...
}
```
#### Async Version
There is no Async version, the async is already built-in **`ActionFilterAttribute`**, **`ResultFilterAttribute`**, and **`ExceptionFilterAttribute`**.
If you need the async version simply implement it directly using [[Asynchronous Filter]] syntax , and then **override the async methods.**
Sample:
```c#
public class SampleActionFilter : ActionFilterAttribute
{
	public SampleActionFilter(type arg1, type arg2, ...)
	{
	}
	
	public override async Task OnActionExecutingAsync(ActionExecutingContext context, ActionExecutionDelegate next)
	{
		//before action method filter logic
		
		await next();
		
		//after action method filter logic
	}
}
```
It needs to be overridden because its implemented as virtual in the parent; assuming you know what that means, if not see [[Modifiers]] and then read the .NET code.
#### Custom Order
**`IOrderedFilter`** is built-in the Filter Attributes, it doesn't need to be inherited, you only need to directly construct in the constructor.
###### So instead of doing this:
```c#
public class SampleFilter : IActionFilter, IOrderedFilter
{
	public int Order {get; set;} //dont get confused, if you auto implement this it will show a lambda.
	
	public SampleFilter(int order)
	{
		//Order = 1; hard coded
		Order = order //or via outside argument
	}
}
```
###### Just do this:
```c#
public class SampleActionFilter : ActionFilterAttribute
{
	public SampleActionFilter(int order)
	{
		//Order = 1; hard coded
		Order = order; //or through argument
	}
}
```
