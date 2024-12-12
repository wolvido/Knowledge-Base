[[Custom Middleware]] | [[Right Order of Middleware]]
Middleware are software components that are used to handle requests and responses as they flow through the request processing pipeline in a web application. 
Essentially, various middlewares can perform work before and after the next middleware in the pipeline.
![[Capture 11.png]]
Middleware can be a delegate or a class if it is more complex. 
Each middleware follows the [[Single Responsibility Principle (SRP)]].

Common uses of middleware in ASP.NET Core:
1. **Authentication and Authorization:** Middleware components like authentication and authorization middleware can be used to handle user authentication and authorization checks.
2. **Routing:** Routing middleware is responsible for mapping incoming requests to the appropriate controller actions in your application.
3. **Logging:** Middleware can log information about each request and response, helping with debugging and monitoring.
4. **Error Handling:** Middleware can capture and handle exceptions and errors in a consistent way.
5. **Compression:** Middleware can compress responses to improve data transfer efficiency.
6. **CORS (Cross-Origin Resource Sharing):** Middleware can be used to handle cross-origin requests, allowing or denying access to resources from different domains.
7. **Security Headers:** Middleware can add security-related headers to HTTP responses to improve web application security.
8. **Session Management:** Middleware can manage user sessions and state between requests.

**NOTE**: Run method short circuits the middlewares and does not forward the request to the next middleware.

Simple Lambda middleware chain sample using `Use` and `Run`.
```c#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();
 
app.Use(async (HttpContext context, RequestDelegate next) =>
{
    await context.Response.WriteAsync("Hello");
    await next(context); //Next passes it to the next middleware, anything below here will be last to run
    await context.Response.WriteAsync("Hello very last"); //this will be skipped and be ran again later
});
 
app.Use(async (HttpContext context, RequestDelegate next) =>
{
    await context.Response.WriteAsync("Hello again");
    await next(context);
});
 
app.Run(async context => //Run terminates everything so it sends the response
{
    await context.Response.WriteAsync("Hello last");
});
```
You can also use **UseWhen()** for conditional middlewares, that will only run when conditions are met see [[Conditional Middleware]]

You can of course run logic in the middle of the middlewares, for example:
```c#
app.Use(async (HttpContext context, RequestDelegate next) =>
{
    await context.Response.WriteAsync("Hello again");
    //(1==2) to simulate that it will not continue next, if condition is not met. Basically a termination.
    if (1 == 2) await next(context); 
});
```
The "Hello again" middleware will be the terminating middleware as the condition will return false.

**NOTES:** 
- the example above is procedural and is not to be followed, just a sample on what to do. To create the correct middleware see: [[Custom Middleware]].
- Right order of middleware must be followed when arranging middleware [[Right Order of Middleware]].
- [[Exception Handling Middleware]] - Handle exceptions from middlewares.
- [[UseExceptionHandler()]] - Handle exceptions and redirect the user to a user friendly error page.


