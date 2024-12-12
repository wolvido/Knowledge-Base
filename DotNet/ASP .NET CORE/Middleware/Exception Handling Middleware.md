Handles exception that come from the Middlewares. It is different from [[Exception Filter]], exception filter covers model binding and the action methods.
Exception Handling Middleware handle everything in the middlewares, including the endpoint middleware.![[Pasted image 20240315152240.png]]
It comes first before all the other middleware except for [[UseExceptionHandler()]], so it can catch and handle all the exceptions that occur in every other middleware.
###### But how does it catch if it comes first? 
Because of the nature of calling middlewares, each middleware must be called as `_next(context)`, so we catch it by putting it inside a try catch:
![[Pasted image 20240315152730.png]]
# How-To:
#### Requirements
- You **may** need to install the `Microsoft.AspNetCore.Http.Abstractions`.
#### File Structure:
Before all that, set up the folder structure.
- In your main project add the folder "Middlewares", store all your custom middleware there.
- Add a new item, and from the list of templates choose Middleware Class.
- Name the file appropriately, for example: "ExceptionHandlingMiddleware". The naming convention is always to add the suffix "Middleware".
#### Syntax
The syntax will be the same as here [[Custom Middleware]], except we add try catch.
```c#
public class ExceptionHandlingMiddleware
{
	private readonly RequestDelegate _next;
	
	public ExceptionHandlingMiddleware(RequestDelegate next)
	{
		_next = next;
	}
	
	public async Task Invoke(HttpContext httpContext)
	{
		try
		{
			await _next(httpContext); //this is why it comes first, so we catch every middleware.
		}
		catch (Exception ex) //ex is an exception context, dont get confused, lookup how to "throw an error" note.
		{
			//catch code and handle it.
		}
	}
}
 
// Extension method used to register the middleware to program.cs
public static class ExceptionHandlingMiddlewareExtensions
{
	public static IApplicationBuilder UseExceptionHandlingMiddleware(this IApplicationBuilder app)
	{
		return app.UseMiddleware<ExceptionHandlingMiddleware>();
	}
}
//when using the middleware template, visual studio uses builder instead of app as variable name, but its the same thing and personally app is better and much less confusing.
```
###### Then simply add this in `Program.cs`
```c#
app.UseExceptionHandlingMiddleware();
```

Don't forget you can always inject whatever you need.
#### Sample:
we will create an exception handler that is designed for the user.
```c#
public class ExceptionHandlingMiddleware
{
	private readonly RequestDelegate _next;
	//we will inject logger and IDiagnosticContext
	private readonly ILogger<ExceptionHandlingMiddleware> _logger;
	private readonly IDiagnosticContext _diagnosticContext;
	
	public ExceptionHandlingMiddleware(RequestDelegate next, ILogger<ExceptionHandlingMiddleware> logger, IDiagnosticContext diagnosticContext)
	{
		_next = next;
		_logger = logger;
		_diagnosticContext = diagnosticContext;
	}
	
	public async Task Invoke(HttpContext httpContext)
	{
		try
		{
			await _next(httpContext); 
		}
		catch (Exception ex)
		{
			if (ex.InnerException != null) //if inner exceptions exist
			{
				_logger.LogError("{ExceptionType} {ExceptionMessage}", //log the inner exceptions
					ex.InnerException.GetType().ToString(), 
					ex.InnerException.Message;
				)
			}
			else //if there are no inner exceptions, log the exceptions as is
			{
				_logger.LogError("{ExceptionType} {ExceptionMessage}",
					ex.GetType().ToString(), ex.Message();
				)
			}
			
			httpContext.Response.StatusCode = 500; 
				//never forget to set the correct status code, since the browser would just assume 200
			await httpContext.Response.WriteAsync("Error Occurred"); //message to the user
			
		}
	}
}
```
###### Now to set this exception handler in production environment:
```c#
if (app.Environment.IsDevelopment())
{
	app.useDevelopmentExceptionPage();
}
else //else, its production
{
	app.UseExceptionHandlingMiddleware(); //set here
}
```
>[!warning] Important
>If you are designing an exception handler for production use, you should use [[UseExceptionHandler()]], it can be used alongside [[Exception Handling Middleware]]. 