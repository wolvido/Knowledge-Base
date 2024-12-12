**what is an endpoint?**
- An endpoint serves as the connection between a URL (the incoming request) and the corresponding code that should be executed to handle that request. 
- Endpoints map the URL to the associated methods, controllers, middleware, or other request handlers in your code.
- For example if the URL is `/home` the routing, routes it to the correct endpoint that will map it to serve the homepage.
syntax:
```c#
public static IApplicationBuilder UseEndpoints(this IApplicationBuilder builder, Action<IEndpointRouteBuilder> configure)
```
###### You can also specify if the endpoint accepts a specific method(get, post, etc.) only:
```c#
app.UseEndpoints(endpoints =>
{
	endpoints.MapPost("/mapPost", async (context) =>
	{
	    await context.Response.WriteAsync("in mapPost");
	});
	 
	endpoints.MapGet("/mapGet", async (context) =>
	{
	    await context.Response.WriteAsync("in mapGet");
	});
});
```

you can also use **`GetEndpoint()`** to get the endpoint:
sample used on a middleware:
```c#
app.Use(async (context, next) =>
{
	Endpoint? endpoint = context.GetEndpoint();
	if (endpoint != null)
	{
		await context.Response.WriteAsync($"Endpoint: {endpoint.DisplayName}\n");
	}
	await next(context);
});
```
# What next:
- [[Endpoint Filters]] - filters for endpoint.