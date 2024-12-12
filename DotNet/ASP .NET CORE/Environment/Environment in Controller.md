Sometimes you have to access the current working environment name programmatically either in the controller or in any other services. To access it in the controller we inject **IWebHostEnvironment**  in the controller, so we can call app.Environment in the controller.
#### Inject **IWebHostEnvironment** in the controller:
```c#
public class HomeController : Controller
{
	private readonly IWebHostEnvironment _env;
	
	public HomeController(IWebHostEnvironment env)
	{
		_env = env;
	}
}
```
Then you can access all the methods from the like app.Environment in program.cs, see [[Environment]] for the various methods and samples or use intellisense.
Sample:
```c#
public IActionResult Index()
{
	if (_env.IsDevelopment() || _env.IsStaging()) //check if environment is development or staging
	{
	    //codes codes
	}
	
	ViewBag.CurrentEnvironment = _env.EnvironmentName; //store current environment name in ViewBag
	
	return View(_cities);
}
```