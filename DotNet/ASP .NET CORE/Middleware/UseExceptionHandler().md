When an exception occurs, redirects to a route that leads to an action method, that may lead to a user friendly error page.
It should be positioned at the earliest possible middleware pipeline, since it is an exception catching middleware.
![[Pasted image 20240318174658.png]]
###### Syntax:
simply add it in `Program.cs`
```c#
if (app.Environment.IsDevelopment())
{
	//dev environment
}
else //else, in production
{
	app.UseExceptionHandler("/RouteToErrorPage"); //simply add the route
}
```
Assuming you know how to make an action method that has an error page.
###### Then in your Controller and Action Method
In order to get the error details, you grab the data from `IExceptionHadlerPathFeature`:
```c#
[Route("RouteToErrorPage")]
public IActionResult ErrorPage()
{
	//any exception that occurs regardless if there are any catch block, will be located in IExceptionHadlerPathFeature.
	IExceptionHandlerPathFeature? exceptionHandlerPathFeature = HttpContext.Features.Get<IExceptionHadlerPathFeature>();
	
	//check if `exceptionHandlerPathFeature` is not null and has error messages
	if (exceptionHandlerPathFeature != null && exceptionHandlerPathFeature.Error != null)
	{
		//if there is, store the error message in View Data to use by the view.
		ViewBag.ErrorMessage = exceptionHandlerPathFeature.Error.Message;
	}
	return View(); 
}
```
Assuming you know how view works, then you can make use of that error message in your view.
>[!warning]
>Carefull to **not** serve sensitive error information to the client.

#### It can also be used alongside [[Exception Handling Middleware]] by re-throwing the error.
- In the catch of your exception handling middleware, simply add throw at the end:
```c#
public async Task Invoke(HttpContext httpContext)
{
	try
	{
		await _next(httpContext); 
	}
	catch (Exception ex)
	{
		//handling codes...
		throw;
	}
}
```
- Then in `program.cs` you can add it alongside:
```c#
if (app.Environment.IsDevelopment())
{
	//dev environment
}
else //else, in production
{
	app.UseExceptionHandler("/RouteToErrorPage");
	app.UseExceptionHandlingMiddleware(); //alogside exception handling middleware
}
```
# What next?
- Learn this, very useful [Handle errors in ASP.NET Core | Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/error-handling?view=aspnetcore-8.0)