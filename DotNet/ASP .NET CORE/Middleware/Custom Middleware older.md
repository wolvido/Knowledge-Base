![[1.png]]
This is the transient older way of implementing a custom middleware.
To create a custom middleware that derives from `IMiddleware`, derive a class from `IMiddleware` and implement its contract
sample:
```c#
public class MyMiddleware : IMiddleware
{
	public async Task InvokeAsync(HttpContext context, RequestDelegate next) //contract
	{
		await context.Response.WriteAsync("custom midware start test");
		await next(context); //moves to the next middleware before executing anything below
		await context.Response.WriteAsync("custom middleware ended and passed on");
	}
}
public static class MyMiddlewareExtension
{
	public static IApplicationBuilder UseMyMiddleware (this IApplicationBuilder app)
	{
		return app.UseMiddleware<MyMiddleware>(); //implement the call method here
	}
}
```
To implement it in program:
```c#
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddTransient<MyMiddleware>(); //if you implement the transient way, you need to add this
var app = builder.Build();
app.UseMyMiddleware(); //the extension method call
```

**how to know which method to use?**
its generally better to use method conventional, and you don't have to register transient.
the transient method is the older style.