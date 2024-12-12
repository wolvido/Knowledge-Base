In order to access [[Configurations]] in the Controller or in a service. It needs to be injected as a service, as is the standard.
# How to implement?
#### Bind it in the Model
First bind your appsettings hierarchy into a model. How? see: [[Options Pattern]].
>[!IF you only need 1 or 2 key-value pair]
IF you only need 1 or 2 key-value pair, then you don't need to bound it and inject it as a service, you can skip to the bottomost example.
#### Register
Once its bound to a model, register that model as a service in program.cs:
```c#
builder.Services.Configure<NameOfModelOptions>(builder.Configuration.GetSection("nameOfTheMasterKey"));
```
>[!question] 
What is the MasterKey? see: [[Options Pattern]] to know.
#### Controller Injection
After registering then you can inject it like any other service.
Sample:
```c#
using Microsoft.Extensions.Options;

public class HomeController: Controller
{
	private readonly NameOfModelOptions _options;
	
	//Injected as a type IOptions<NameOfModelOptions>
	public HomeController(IOptions<NameOfModelOptions> nameOfModelOptions)
	{
		_options = nameOfModelOptions.Value;
	}
	
	public IActionResult Index()
	{
		//store the config value in the ViewBag MyKey
		ViewBag.MyKey = _options["Key"]; 

		//You can also supply default value if key does not exist
		ViewBag.MyKey = _options.GetValue("Key", "defaultValue");
		
		return View();
	}
	
}

```
#### How to inject configuration in a service
You can inject it in the service class directly without using options pattern:
```c#
public class CityWeatherApiService : ICityWeatherService
{
	private readonly IConfiguration _configuration;
	
	public CityWeatherApiService(Iconfiguration configuration)
	{
		_configuration = configuration;
	}

	//you can access it the same way as samples above
	var apiKey = _configuration["secretApiKey"];
}
```


---

IF you only need 1 or 2 key-value pair, then you dont need to bound it and register as a service, It might be better to just inject IConfiguration and use it method style. But be warned, this is not extensible. Use this if you know what you're doing.
sample:
```c#
public class HomeController : Controller
{
	private readonly IConfiguration _configuration;
	public HomeController(IConfiguration configuration)
	{
		_configuration = configuration;
	}

	public IActionResult Index()
	{
		ViewBag.MyKey = _configuration["Key"]; //store the config value in the ViewBag MyKey
		
		//You can also supply default value if key does not exist
		ViewBag.MyKey = _configuration.GetValue("Key", "defaultValue");
		
		return View();
	}
}
```














