A specific scope inside of the service that handles the methods inside the service, instead of scope that handles the service itself(Transient, Scoped, or Singleton scope).
For example your service creates a DB connection, and that DB connection needs to be destroyed when its done being used instead of waiting for the whole service to be destroyed by Transient, Scoped, or Singleton scope
>[!Warning] 
><mark style="background: #FF5582A6;">Do Not Implement this</mark> when using entity framework.
>If you are using Entity Framework, disposing will be handled by the framework automatically. Only use this for non entity framework or you are making your own code for DB connections.
# How?
### Switch to scope
First you must switch the IoC Container scope to scoped:
```c#
builder.Services.AddScoped<ISampleService, SampleService>();
```
### Create a Dispose method
Service should inherit from **`IDisposable`** and implement its own Dispose method
```c#
public class SampleService : ISampleService, IDisposable
{
    public void Dispose()
    {
        // add logic to dispose a db connection or file handles or network connections etc..
    }
}
```
### IServiceScopeFactory and Using
Now if you need that DB connection or File Handling to close itself when its done processing, you need to `IServiceScopeFactory` to the controller.
First inject `IServiceScopeFactory` in the controller:
```c#
public class HomeController : Controller
{
    private readonly ISampleService _sampleService;
	private readonly IServiceScopeFactory _serviceScopeFactory; //set up the field

	//then add an IServiceScopeFactory type in the constructor parameters-
	//IoC will automatically inject an object of type IServiceScopeFactory
    public HomeController(ISampleService sampleService, IServiceScopeFactory serviceScopeFactory)
    {
        _sampleService = sampleService;
        //then ofcourse assign the IServiceScopeFactory object to the field to succesfully inject it
        _serviceScopeFactory = serviceScopeFactory;
    }

    [Route("/")]
    public IActionResult Index()
    {
    	//Then in the action method, we need to use using keyword to properly use the Dispose
	    using (IServiceScope scope = _serviceScopeFactory.CreateScope())
	    {
		    //Inject the Service into this scope
		    ISampleService sampleService = scope.ServiceProvider.GetRequiredService<ISampleService>();
		    //This code above^ is equal to injecting the service in the constructor but-
		    //instead we are injecting it as part of this child scope

			//Now you have an instance of the service
			//add your DB or your file handling or network connection code here along with the-
			//service instance
		    
	    }
	    //when the using block is finished, it will automatically call the Dispose method and-
	    //dispose the DB or your file handling or network connection as soon as it is done.
	    
		return View();
    }
}
```
see: [[Using]] for more details.
With this method your DB connection or your file handling or network connection will be closed as soon as it is done.
