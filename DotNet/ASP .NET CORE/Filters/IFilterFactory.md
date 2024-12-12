It can be used to create Filters in a Factory pattern(see: [[Class Factories]]), but fucking bullshit harsha course only teaches a very specific use-case, which is to combine the easy use of [[Filter Attribute]] but with the ability to inject dependencies, but whatever, fine let's learn that. (This is really hacky, but maybe it can be used, idk).

So, in [[Filter Attribute]] you can apply the filter directly without using very long and hard to read **`TypeFilter`**, but you will not be able to inject anything, not even the logger, the workaround is to use **`IFilterFactory`** and **`Attribute`**.
>If you don't know what I'm talking about, see [[Filter Attribute]] first.
# How-To:
First, is you just make a normal filter, not a [[Filter Attribute]], but create it in a way that the argument properties are public and the constructor does not construct the arguments.  Bare with me, this shit is hacky.
The goal here is to let the Factory receive the arguments then it can directly set the properties of **`SampleActionFilter`**.
```c#
public class SampleActionFilter : IActionFilter
{
    public string SampleArg1 {get; set;}
	public int SampleArg2 {get; set;}
	
	//injection will be private
	ptivate readonly ISampleInjection _sampleInjection;
    
    public ShoppingCartController(ISampleInjection sampleInjection)
    {
	    _sampleInjection = sampleInjection;
	    //notice we did not include the arguments in the constructor only the injections.
    }
	
	//The methods will remain the same
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
You can also create it in [[Asynchronous Filter]] version, just keep the argument properties public and the constructor does not construct the arguments.
###### Then, you create the filter factory class in the same file, just above the filter class.
- The naming convention is usually to postfix it with "FilterFactoryAttribute".
- We will also inherit from **`Attribute`** and  **`IFilterFactory`**.
```c#
public class SampleFilterFactoryAttribute : Attribute, IFilterFactory
{
	public bool IsReusable => False; // or True, indicates if the filter object we create here is reusable by other requests.
		//False by default.
	
	//properties of the original Filter Class and the injection
	private string? SampleArg1 { get; set; }
	private string? SampleArg2 { get; set; }
		
	public SampleFilterFactoryAttribute(string sampleArg1, int sampleArg2)
	{
		_sampleArg1 = sampleArg1;
		_sampleArg2 = sampleArg2;
	}
	
	//this will create the filter object of the original Filter Class and assign the values
	public IFilterMetadata CreateInstance(IServiceProvider serviceProvider)
	{
		var filter = serviceProvider.GetRequiredService<SampleActionFilter>(); //inject the original Filter Class
		
		//assign the values of the arguments to the object of the Filter Class
		filter.SampleArg1 = _sampleArg1;
		filter.SampleArg2 = _sampleArg2;
		
		return filter;
	}
}

//below here is the original filter class
//public class SampleActionFilter : IActionFilter
{
...
}
```
###### Then it needs to be registered to the program.cs in a different way, not the same way as the original [[Global Level Filters]].
>I told you this was hacky.
```c#
builder.Services.AddTransient<SampleActionFilter>();

builder.Services.AddControllersWithViews(options => {
	options.Filters.Add(new SampleActionFilter() {SampleArg1 = arg1, SampleArg2 = arg2}); 
		//dont get confused, arg1 and arg2 are variables with data on it, or it can be hard coded
		
	//instead of-
	//options.Filters.Add(new SampleActionFilter(arg1,arg2));
		//since we the structure of SampleActionFilter is that the properties are directly accessed
});
```
This is only for [[Global Level Filters]], no need to do this if not global. 
###### Now simply implement it directly as an attribute without using **`TypeFilter`**:
```c#
[SampleFilterFactoryAttribute(sampleArg1, sampleArg2)]
public async Task<IActionResult> Index()
{
	//codes...
}
```
Essentially it will first invoke the Filter Factory then the Original Filter Class.
>Controller -> Filter Factory -> Filter Class.
###### Can be used exactly like [[Filter Attribute]] but can be injected with.
>[!info]
>Personally, I think the hackiness of this is not worth it, I think its better to use just  **`TypeFilter`**. It is long, but it's uniform.
