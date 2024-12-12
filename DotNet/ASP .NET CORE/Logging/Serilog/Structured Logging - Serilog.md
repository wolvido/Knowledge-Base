Its not a good practice to log static messages that don't change. Try to use interpolation in your logs, so the log messages can be dynamic. see: [[concatenation vs interpolation]].
###### Sample:
```c#
public class HomeController : Controller
{
	public IActionResult Index()
	{
		_logger.LogInformation("We are in HomeController/Index");
	}
}
```
###### The sample above is using a static log, that is bad practice, instead you can do:
```c#
public class HomeController : Controller
{
	public IActionResult Index()
	{
		_logger.LogInformation("We are in {ControllerName}/{ActionMethodName}", nameof(HomeController), nameof(Index));
	}
}
```
Any other specific details that can be provided by the program, you need to use structured logging. I don't think I need to explain why.