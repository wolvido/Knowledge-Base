
![[Capture 12.png]]
There are two ways to create a custom middleware
1.  the conventional way
2.  the transient way that requires deriving from `IMiddleware` it is and older way, see [[Custom Middleware older]]
#### Folder Structure:
Before all that, set up the folder structure.
- In your main project add the folder "Middleware", store all your custom middleware there.
###### The conventional way:
```c#
public class MyMiddleware
{
	//inject RequestDelegate
	private readonly RequestDelegate _next;
	public Middleware(RequestDelegate next)
	{
		_next = next;
	}
	
	public async Task Invoke(httpContext context)
	{
		await context.Response.WriteAsync("custom middleware start");
		
		await _next(context); //call the next middleware
		
		await context.Response.WriteAsync("called middleware have ended");
	}
}
```
###### To implement it in **program main** we will create an extension method.
Add this class at the bottom of the custom MyMiddleware class.
```c#
public class MyMiddleware
{
	//...
}
//add at the bottom
public static class MyMiddlewareExtension
{
	public static IApplicationBuilder UseMyMiddleware (this IApplicationBuilder app)
	{
		return app.UseMiddleware<MyMiddleware>(); //implement the call method here
	}
}
//when using the middleware template, visual studio uses builder instead of app as variable name, but its the same thing and personally app is better and much less confusing.
```
basically instead of adding `app.UseMiddleware<MyMiddleware>();` in program main, we contain it in an extension so we can call it like a method of app because it follows the convention.
**Note**: if you're wondering why we use `IApplicationBuilder` as a return because  `var builder = WebApplication.CreateBuilder(args);` is of type `WebApplication` and  `WebApplication` is derived from `IApplicationBuilder`. `IApplicationBuilder` is the one with the extension `.UseMiddleware<Middleware>();`. So we use `IApplicationBuilder` to be able to use `.UseMiddleware<Middleware>();`.

**In program main:**
```c#
app.UseMyMiddleware(); //call the extension directly, instead of `app.UseMiddleware<MyMiddleware>();`
```
> it's more of a general practice, since `IApllicationBuilder` already has a lot of methods, it looks similar to just call it like a method of app.
