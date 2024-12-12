#### Global State in Services
- Avoid using static classes to store some data globally for all users/request.
- If you want to store some Global state data in a singleton service, and if the data is a simple and in small amount use Concurrent Dictionary for Dictionary and Use Concurrent Bag for List, because they handle simultaneous operations better via multiple threads. Which means they are thread safe. 
- If you want to store large amounts of data for Global, use Distributed Cache/Redis, for any significant amount of data or complex scenarios.
#### Request State in Services
- You are not suppose to share data from one scoped service to another. That means from one service class to another. Because they are not thread-safe.
- Use **`HttpContext.Items `** instead if you need to.
#### Service Locator Usage
Do not use the service locator pattern for injecting services
```c#
ISampleService sampleService = scope.ServiceProvider.GetRequiredService<ISampleService>();
```
Only use it on a child scope or [[Service Scope]].
Instead just inject normally in the controller.
#### DO NOT call Dispose
Do not call the dispose method of a service manually. Its the job of the [[IoC]] Container.
#### DO NOT create captive dependencies
That means injecting scoped or transient services in singleton services.
A service should never depend on a service that has a shorter lifetime than its own, that will cause some bad shite.
In a Transient or Scoped service, you can inject Transient, Scoped, or Singleton, but in a Singleton Service you cannot inject Transient and Scoped, only Singleton.
#### Using Reference of a service instance
Do not use a reference of a service instance outside of the controller or class.
For Example: 
```c#
public class HomeController : Controller
{
    public readonly ICitiesService _citiesService;
    //normally this field would be set as private to prevent the problem
    //but when this field injection is set to public and-
    //used outside the controller, it is anti pattern and-
    //will cause error of the field has been disposed.
 
    public HomeController(ICitiesService citiesService)
    {
        _citiesService = citiesService;
    }
 
    [Route("/")]
    public IActionResult Index()
    {
		//code whatever
		return View();
    }
}
```
Essentially do not set a service injection field into public, always private.