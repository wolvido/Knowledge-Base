![[Pasted image 20240301210417.png]]
If the image confuses you, I suggest going back to [[Action Filter]].
###### For example, your action filter needs accept two parameters, var1 and var2:
```c#
public class HomeController : Controller
{
	[TypeFilter(typeof(SampleActionFilter), Arguments = new object[] {Parameter1, Parameter2} )]
	public IActionResult Index()
	{
	}
	//dont get confused, Parameter1 and Parameter2 are variables with data
}
```
In your action filter:
```c#
public class SampleActionFilter : IActionFilter
{
	private readonly string _var1;
	private readonly int _var2; 
	
	public SampleActionFilter(string var1, int var2)
	{
		_var1 = var1;
		_var2 = var2;
	}
}
```
###### The sample above is simplistic, more real sample would be:
```c#
public class HomeController : Controller
{
	[TypeFilter(typeof(LoggingActionFilter), Arguments = new object[] {LogLevel.Info, LogLevel.Debug} )]
	public IActionResult Index()
	{
	}
}
```
##### Also see injecting in Filters [[Inject to a Filter]]