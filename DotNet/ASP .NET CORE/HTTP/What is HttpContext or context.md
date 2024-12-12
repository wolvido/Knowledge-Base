---
keywords: |-
  what is context net core
  how to get data from url
  how to access context data
---
>[!info]
>The samples below are not to be used in real world use, you need to use [[Model Binding]] for extracting data from route.

HttpContext represents the current HTTP request and response in your application. 
- You don't explicitly create or destroy the `HttpContext` object in your code. It's created for you at the start of the request and automatically cleaned up at the end of the request.
- The `HttpContext` object has properties of various aspects of the current request and response, such as headers, query parameters, form data, and more.  see: [[HTTP Request]], [[HTTP Response]] for more info on request and response. These properties are assigned for every request or response, an `HttpContext` is initialized for every request or response.
- Built-in Middleware classes and Controller classes is dependency injected by .net core of an object of `HttpContext`, their built-in extension methods utilizes the object and assign it the `context` keyword or `ControllerContext.HttpContext` for controllers, or for custom middlewares it is injected and assigned as `context` keyword (see [[Custom Middleware]] for more info) .

Sample in a Controller:
```c#
public class SampleController : Controller
{
    [Route("/hello")]
    public IActionResult SampleActionMethod()
	{
		//in base controller class, the HttpContext object is assigned in HttpContext.
		//you only need to call it like so:
		if (HttpContext.Request.Query.ContainsKey("1"))
		{
			return Content("Hello from Controller", "text/plain");
		}
		//Request is already assigned in ControllerBase as an HttpRequest Type from HttpContext.
		//So you can also just do this instead:
		if (Request.Query.ContainsKey("1"))
		{
			return Content("Hello from Controller", "text/plain");
		}
	 }
}
```
Sample in a custom middleware:
```c#
public class MyCustomMiddleware
{
	private readonly RequestDelegate _next;
	public Middleware(RequestDelegate next){_next = next;}
	
	public async Task Invoke(httpContext context) //An object of the HttpContext is injected here
	{
		//HttpContext object is assigned as context parameter, so it is used like so:
		await context.Response.WriteAsync("custom midware start test/n");
		await _next(context);
		await context.Response.WriteAsync("custom middleware ended and passed on/n");
	}
}
```
To access data from context in a controller:
```c#
public class SampleController : Controller
{
    private readonly IHttpContextAccessor _httpContextAccessor;
    public SampleController(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }
    
    public IActionResult GetRequestData()
    {
        // Access the HttpContext from the injected IHttpContextAccessor
        var httpContext = _httpContextAccessor.HttpContext;
        
        // Access various request data
        var requestPath = httpContext.Request.Path;
        var userAgent = httpContext.Request.Headers["User-Agent"];
        var remoteIpAddress = httpContext.Connection.RemoteIpAddress;
        var queryString = httpContext.Request.QueryString.Value;
        
        // Example of accessing query parameters
        var queryParameter = httpContext.Request.Query["parameterName"];
        
        // Example of accessing form data if it's a POST request
        if (httpContext.Request.Method == "POST")
        {
            var formDataValue = httpContext.Request.Form["formFieldName"];
        }
        
        // Set response information
        httpContext.Response.StatusCode = 200;
        httpContext.Response.Headers.Add("Custom-Header", "Hello, World!");
        
        return View();
    }
}
```
also see: [[Check Route Parameter Value]].

The `HttpContext` object in ASP.NET Core is not directly created by your code. Instead, it's created and managed by the ASP.NET Core framework as part of the request processing pipeline. Here's how it works:
1. **Request Comes In:** When an HTTP request is received by your ASP.NET Core application, the ASP.NET Core framework processes the request.
2. **Middleware Pipeline:** The request passes through a series of middleware components configured in your `Startup.cs` file. Middleware components are responsible for various tasks like routing, authentication, and more.
3. **HttpContext Creation:** As the request flows through the middleware pipeline, the `HttpContext` object is created by the ASP.NET Core framework. This object is initialized with information about the current request and response. It represents the context of the ongoing HTTP request.
4. **Middleware Manipulation:** Each middleware component in the pipeline can read and modify the `HttpContext`. They can add data to it, modify request and response details, and perform various tasks as needed.
5. **Request Handling:** When the request has passed through all the middleware components and a controller action (if applicable) is invoked, the `HttpContext` is still available for use within your code.
6. **Response Sent:** Once the response is generated and sent back to the client, the `HttpContext` is disposed of, and any data associated with that particular request is cleaned up. This disposal is automatic and part of the ASP.NET Core framework's request handling process.

You don't explicitly create or destroy the `HttpContext` object in your code. It's created for you at the start of the request and automatically cleaned up at the end of the request. This is a key part of the ASP.NET Core request handling architecture, which abstracts away much of the low-level details of request processing and allows you to focus on building your application's features.

