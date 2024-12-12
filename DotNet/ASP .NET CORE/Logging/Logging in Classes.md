---
keywords: how to inject logger
---
Writing actual log in Controllers, Services, Repository, and other classes.
# How-To:
You inject it using **`ILogger`** Interface. 
#### The logging methods are:
```c#
_logger.LogDebug("debug message");
_logger.LogInformation("log info");
_logger.LogWarning("warning");
_logger.LogError("error");
_logger.LogCritical("critical info");
```
see [[Logging]], if you forgot the purpose of each.
#### Controller
Inject it in the controller
```c#
public class HomeController : Controller
{
	private readonly ILogger<HomeController> _logger;
	
	public HomeController(ILogger<HomeController> logger)
	{
		_logger = logger;
	}
}
```
for example, we want to log what happens to index action method that accepts various parameters:
```c#
public IActionResult Index(string? searchBy, string? searchString)
{
	//write some info saying the user is in HomeController index action
	_logger.LogInformation("HomeController Index action method");
		//If you see this log, then you understand the user is in HomeController Index
	
	//In debug logging level, I want to know what were the inputs provided
	_logger.LogDebug($"searchBy: {searchBy}, searchString: {searchString}");
		//we used LogDebug because they will be usefull later when debugging
		//dont forget the purpose of logging is to find out what went wrong
	
	//codes for the index method etc...
}
```
Depending on the actions of a method, add logs as much as possible, like a newbie adding console.writelines.
>[!warning] In the sample above we used static logs, its not a good practice to log static messages that don't change, try to use [[Structured Logging - Serilog]].
#### Service
The service its the same, you just have to inject.
```c#
 public class PersonsService : IPersonsService
 {
	 private readonly ILogger<PersonsService> _logger;
	 
	 public PersonsService(ILogger<IPersonsService> logger)
	 {
		 _logger = logger;
	 }
 }
```
For example in persons service, you have a service method you need to log:
```c#
	public async Task<List<Person>> GetAllPersons()
	{
	   _logger.LogInformation("GetAllPersons of PersonsService");
		   //logs that user is using GetAllPersons of PersonsService
	}
```
##### Not only do you use LogInformation() or LogDebug(), you should add the other loggng methods as well, depending on what you need. Remember: Log necessary details as much as possible, like a newbie adding console.writelines.
>[!warning] Again, In the sample above we used static logs, its not a good practice to log static messages that don't change, try to use [[Structured Logging - Serilog]].
#### Repository
I think you already know how to do it in repo, its the same as above.