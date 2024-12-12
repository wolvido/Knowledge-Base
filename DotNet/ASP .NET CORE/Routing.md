---
keywords: |-
  how to handle url
  how to handle links
---
**What is Routing?**
Checks for http method and url, and then connecting them to the correct endpoints
![[Capture 14.png]]
There are two types of routing supported by ASP.NET Core

1. The conventional routing- In conventional routing, you typically configure your routes in the Program.cs file using a route template. Endpoints are usually used.
2. Attribute routing- Using controllers. see [[Controllers]]
see [[When to use conventional or attribute routing]]

**sample for conventional routing:**
```c#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();
 
app.UseRouting(); //necessary to enable the routing system including endpoints
 
app.UseEndpoints(endpoints =>
{
	endpoints.Map("/home", async (context) =>
	{
		await context.Response.WriteAsync("in homepage"); //simulated homepage handler
	});
	
	endpoints.Map("/about", async (context) =>
	{
		await context.Response.WriteAsync("in about page"); //simulated about page handler
	});
});
```
**How endpoint works?** see [[Endpoint]] for more info on routing.

**Why do we need to add `UseRouting()` at the start?**
When you add `app.UseRouting();` to your middleware pipeline, you are configuring the application to use ASP.NET Core's routing system to process incoming HTTP requests. This middleware is essential for URL routing, which means it determines which endpoint should handle a particular request based on the URL's path and other route values.
1. **URL Routing:** It allows the application to analyze incoming request URLs and match them to predefined route patterns.
2. **Endpoint Matching:** It is responsible for matching incoming requests to the defined endpoints, which specify how to process the request, including which action methods to execute.
3. **Route Parameters:** It extracts route parameters from the request URL and makes them available for use in the associated action methods.
4. **Middleware Processing:** After routing has determined the appropriate endpoint, the request is then passed to the next middleware components in the pipeline for further processing.

**If it is so important, why do we need to explicitly code it, why not just run it automatically?**
Here are some reasons:
1. **Flexibility**: ASP.NET Core emphasizes flexibility and configurability. By explicitly adding `app.UseRouting();` to your middleware pipeline, you have control over the order of execution and can customize routing to your application's specific needs.
2. **Customization**: You may need to customize routing behavior, such as adding custom route constraints, handling special cases, or integrating third-party routing libraries. The ability to configure routing explicitly allows you to make these adjustments.
3. **Modularity**: ASP.NET Core is designed as a modular framework where you pick and choose the middleware components you need. Not every application requires routing, so it's up to the developer to include it in the pipeline if necessary.
4. **Clarity**: Explicitly adding routing middleware to your pipeline makes the code more readable and self-documenting. It's clear to other developers what is happening in the request handling process.
#### what next?
- If you want to know which route url comes first see: [[Endpoint Selection]]
- Instead of having to manually creating routes in a controller or action method, you can use route attributes to set it to the name of the action method or controller. You can also specify what verb requests the route will accept. see: [[Attribute Routing]].
