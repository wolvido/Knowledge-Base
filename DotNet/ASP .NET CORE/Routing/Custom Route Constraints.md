To create a custom constraint you create a class that inherits from `IRouteConstraint`:
```c#
public class MyCustomConstraint : IRouteConstraint
{
    public bool Match(HttpContext? httpContext, IRouter? route, string routeKey, RouteValueDictionary values,
        RouteDirection routeDirection)
    {
        // Implement your custom validation logic here. 
        // Return true if the route parameter is valid, and false if it's not. 
        // You can access route values using values[routeKey]. 
        // You can also access the HttpContext to perform validation based on the request.
    }
}
```
Values explained:
1. **`HttpContext` (httpContext):** The `HttpContext` object represents the current HTTP request. It provides access to information about the incoming request, such as headers, cookies, query parameters, and the request's method. In the context of a custom route constraint, you might use it to access information from the request to assist with your validation logic. For example, you might use it to inspect request headers or query parameters to make decisions about the route constraint.
2. **`IRouter` (route):** The `IRouter` is responsible for generating URLs and matching routes. It is typically not used, it is only used on for more advanced scenarios where the custom route constraint may need to interact with the router to influence URL generation or route matching.
3. **`string` (routeKey):** The `routeKey` is the name of the route parameter that the constraint is applied to.  For example: `{parameter:constraintName}` syntax. `routeKey` represents the name of the parameter (e.g., "parameter" in `{parameter:constraintName}`). Its simply the name of the value, not the value itself.
5. **`RouteValueDictionary` (values):** `values` is a dictionary that holds the route values for the current route. For example if you have the route `"products/{id:int}"`, then `values['id']` would contain the `int`. This is the value you will validate against your custom constraint.
7. **`RouteDirection` (routeDirection):** This parameter specifies the direction in which route matching is occurring. The `RouteDirection` enum has two values: `RouteDirection.IncomingRequest` and `RouteDirection.UrlGeneration`. In the context of a route constraint, you can use `routeDirection` to determine whether the route constraint is being evaluated for an incoming request (URL matching) or URL generation. For most constraints, you can check if `routeDirection` is `RouteDirection.IncomingRequest` to ensure that your constraint logic is applied only when processing incoming requests.

Then after that you add the logic, sample:
```c#
public class MyCustomConstraint : IRouteConstraint
{
	public bool Match(HttpContext? httpContext, IRouter? route, string routeKey, RouteValueDictionary values,
		RouteDirection routeDirection)
	{
		if (values[routeKey] == null) return false; //if parameter is empty then constraint not passed
		
		var customConstraintValue = Convert.ToString(values[routeKey]); //convert the value to a data type
		//in this case, the constraint is that we can only pass the word "test", if not constraint is not passed
		if (customConstraintValue != "test") 
		{
			return false;
		}
		return true;
	}
}
```
**Note**: you can also use `routeDirection`, `httpContext`, and `route` to create your constraint, not just `values` and `routeKey`, depending on the goal.

After that, then, In order for it to be recognized by the build, you should add this code:
```c#
builder.Services.AddRouting(options =>
{
    options.ConstraintMap.Add("customConstraint", typeof(MyCustomConstraint));
});
```
Add this^ to your program.cs and **make sure you add it before you build the app**, or else will throw an error.
in other words, add it before`var app = builder.Build();`

If your still confused on how this all works, remember how your just providing the implementation to be handled, by hander. It is simply injected like a delegate.

![[Capture 18.png]]
