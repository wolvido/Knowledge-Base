This is where we [[Filter Short Circuit]] the pipeline if exceptions is caught in the processing of an HTTP request, which is the model binding, controller creation, action methods, and all the filters of the mentioned processes. Exception filters are specifically designed, where they can intercept and handle exceptions that occur during the processing of an HTTP request before it reaches the IActionResult execution.
![[Pasted image 20240307162609.png]]
**If Exceptions are raised in authorization, resource filter, result filter and `IActionResult`; exception filter will not catch it.**
If you need to catch exceptions in the area outside of request processing, you will need an exception middleware. see: [[Exception Handling Middleware]] and if you need to handle it in production environment, see [[UseExceptionHandler()]].
###### Purpose of exception filter:
- Handles exceptions that occur in the model binding, controller creation, action method, and all their filters.
- Will not handle the exceptions in authorization, resource filter, result filter and `IActionResult`. Those are handled by [[Exception Handling Middleware]] or if you need to handle it in production environment, see [[UseExceptionHandler()]].
  Exception filters are specifically designed, where they can intercept and handle exceptions that occur during the processing of an HTTP request before it reaches the IActionResult execution.
- Only recommended to be used when you want a different error handling for a specific controller, otherwise use [[Exception Handling Middleware]], and if you need to handle it in production environment, see [[UseExceptionHandler()]].
# How-To:
**Assuming you know how to make filters and its folder and how to attribute it**, if not read again [[Filters]].
###### Syntax:
```c#
public class SampleExceptionFilter : IExceptionFilter
{
	//Its necessary to inject IHostEnvironment in order to know what environment the filter is running
	//this way we can prevent exception messaged from appearing in production environment with the users
	public HandleExceptionFilter(IHostEnvironment hostEnvironment)
	{
		_hostEnvironment = hostEnvironment;
	}
	
	public void OnException(ExceptionContext context)
	{
		//exception handling logic here
		
		if (_hostEnvironment.IsDevelopment()) //short circuit only in development environment
		{
			//short circuit
			context.Result = //do something
			
			//or in some cases
			context.ExceptionHandled = true;
		}
	}
}
```
For the Asynchronous syntax:
```c#
public class SampleExceptionFilter : IAsyncExceptionFilter
{
	public HandleExceptionFilter(IHostEnvironment hostEnvironment)
	{
		_hostEnvironment = hostEnvironment;
	}
	
	public void OnExceptionAsync(ExceptionContext context)
	{
		//exception handling logic here
		
		if (_hostEnvironment.IsDevelopment()) //short circuit only in development environment
		{
			//short circuit
			context.Result = //do something
			
			//or in some cases
			context.ExceptionHandled = true;
		}
		return Task.CompletedTask;
	}
}
```
###### Don't forget; Like every other filter, the context will always contain what data you need to set or use for your logic.