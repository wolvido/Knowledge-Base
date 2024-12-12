Syntax:
```c#
public class SampleActionFilter : IActionFilter
{
    private readonly ISampleInjection _sampleInjection;
    
    public ShoppingCartController(ISampleInjection sampleInjection)
    {
        _sampleInjection = sampleInjection;
    }
	
	public void OnActionExecuting(ActionExecutingContext context)
	{
		//code that will execute before the action method
	}
	public void OnActionExecuted(ActionExecutedContext context)
	{
		//code that will execute after the action method
	}
}
```
###### Injecting Logger:
```c#
public class SampleActionFilter : IActionFilter
{
	private readonly ILogger<SampleActionFilter> _logger;
	
	public SampleActionFilter(ILogger<SampleActionFilter> logger)
	{
		_logger = logger;
	}
	
	public void OnActionExecuted(ActionExecutedContext context)
	{
		//code that will execute after the action method
	}
	public void OnActionExecuting(ActionExecutingContext context)
	{
		//code that will execute before the action method
	}
}
```

Then of course, you need to register it in program.cs, through the `builder.Services.BuildServiceProvider().GetRequiredService`.
 For example if your filter is using a logger:
```c#
builder.Services.AddControllersWithViews(options => {
	var logger = builder.Services.BuildServiceProvider().GetRequiredService<ILogger<NameOfFilter>>();
	options.Filters.Add(new NameOfFilter(logger, argument1, argument2))
});
```
Not just logger, you can get any service injected.