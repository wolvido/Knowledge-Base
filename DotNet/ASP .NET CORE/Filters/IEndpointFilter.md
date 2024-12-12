Create a separate class for your [[Endpoint Filters]] instead of cluttering the Endpoints. This class will inherit from `IEndpointFilter`.
# How-To:
- Assuming you already have a "Filters" folder. If not make one, in [[Clean Architecture]] store it in the [[UI Layer]].
- Inside "Filters" folder create the "EndpointFilters" folder.
###### Syntax:
```c#
public class SampleEndpointFilter : IEndpointFilter
{
	public ValueTask<object?> InvokeAsync(EndpointFilterInvocationContext context, EndpointFilterDelegate next)
	{
		//before endpoint logic
		
		var result = await next(context); //invokes the next endpoint filter or endpoint delegate.
		//don't get confused, delegate just means endpoint, endpoint is the one the filter is trying to filter.
		
		//After endpoint logic
		
		return result;
	}
}
```
###### Sample, implementing a logger:
```c#
public class LoggerEndpointFilter : IEndpointFilter
{
	private readonly ILogger<CustomEndpointFilter> _logger;
	
	public CustomEndpointFilter(ILogger<CustomEndpointFilter> logger)
	{
		_logger = logger;
	}
	
	public async ValueTask<object?> InvokeAsync(EndpointFilterInvocationContext context, EndpointFilterDelegate next)
	{
		//Before logic
		_logger.LogInformation("Endpoint filter - before logic");
		
		var result = await next(context); //It invokes the subsequent filter or endpoint's request delegate
		
		
		//After logic
		_logger.LogInformation("Endpoint filter - after logic");
		
		return result;
	}
}
```
#### How to Apply the Filter?
Similar way to the [[Endpoint Filters]], you apply on it's built in method `.AddEndPointFilter<nameOfFilter>`, sample:
```c#
app.MapPost("/route", async (HttpContxt context, Model modelToPost) => {
	//...
}).AddEndpointFilter<LoggerEndpointFilter>();
```