While [[Action Filter]] filters the processes of the action method, and [[Result Filter]] filters the result of the action method, **Resource Filter** filters the whole pipeline including  [[Model Binding]], except [[Authorization Filter]] of course. Also filters the other filter.
![[Screenshot 2024-03-06 at 17-53-54 Asp.Net Core 8 (.NET 8) True Ultimate Guide 1.png]]
###### What is its purpose?
It filters the **resource**. What is **"resource"**? 
Essentially it is the result plus with everything else, so if [[Result Filter]] only filters result, **Resource Filter** filters the result plus the logging, the cleanup operations, and the response transformation. So anything that comes in and out of the whole pipeline with modifications from the filters.
- It can do some work before [[Model Binding]].
- modify the process of model binding.
- Short circuit the whole pipeline. see: [[Filter Short Circuit]].
- Read the response body and store it in cache.
**NOTE**: In general it is very rare to use Resource Filter, it is mostly used to read and store the response body in cache.
# How-To:
The creation works the same as [[Action Filter]], the difference is in method name, the interface, and the folder location.
- First, in your Filters folder, create the folder "ResourceFilters".
Syntax:
```c#
public class SampleResourceFilter : IResourceFilter
{
	public void OnResourceExecuting(ResourceExecutingContext context)
	{
		//code that will execute before the response is sent
	}
	public void OnResourceExecuted(ResourceExecutedContext context)
	{
		//code that will execute after the response is sent
	}
}
```
This is the non-async version, don't forget, you can also [[Asynchronous Filter]].
###### Also, don't forget, you can always access or modify anything in the **`ActionExecutedContext`** for whatever logic you need.

###### To short circuit you use context.Result:
```c#
public class SampleResourceFilter : IResourceFilter
{
	public void OnResourceExecuting(ActionExecutingContext context)
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
