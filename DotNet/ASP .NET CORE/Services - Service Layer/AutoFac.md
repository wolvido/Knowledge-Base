By default NetCore has a built in IoC(Inversion of Control Container)[[IoC]]. 
**Autofac** is an open source alternative to IoC. It is not required to use this, best practice is to use default, then when you think the default cant handle the requirements, use Autofac, if you think Autofac cant handle, then use those even more advanced than Autofac.
![[Autofac.png]]
# How to use and enable Autofac?
- To add it you right click on dependencies, then manage nuget packages, then browse, then search autofac, install autofac by Autofac Contributors.
- Then search and install autofac.Extensions.DependencyInjection
- Then in Program.cs add:
```c#
using Autofac;
using Autofac.Extensions.DependencyInjection;

//make sure you add this code below builder initialization
builder.Host.UseServiceProviderFactory(new AutofacServiceProviderFactory());
```
#### How to Register Services?
In order to register the services you use:
```c#
builder.Host.ConfigureContainer<ContainerBuilder>(builder =>
{
    builder.RegisterType<SampleService>().As<ISampleService>().InstancePerDependency();
});
```
the code above is equal to:
```c#
builder.Services.AddTransient<ISampleService, SampleService>();
```
Scopes:
- InstancePerDependency = transient 
- InstancePerLifetimeScope = Scoped
- SingleInstance = Singleton  
InstancePerOwned = Lifetime of the service is based on the relations between the classes. Essentially one instance of the service per relationship.
InstancePerMatchingLifetimeScope = One instance per matching name.

#### Service Scope
What if I need a Service Scope like [[Service Scope]]?
###### In the Controller instead of this:
```c#
public class HomeController : Controller
{
    private readonly ISampleService _sampleService;
	private readonly IServiceScopeFactory _serviceScopeFactory; 

    public HomeController(ISampleService sampleService, IServiceScopeFactory serviceScopeFactory)
    {
        _sampleService = sampleService;
        _serviceScopeFactory = serviceScopeFactory;
    }

    [Route("/")]
    public IActionResult Index()
    {
	    using (IServiceScope scope = _serviceScopeFactory.CreateScope())
	    {
		    ISampleService sampleService = scope.ServiceProvider.GetRequiredService<ISampleService>();
	    }  
		return View();
    }
}
```
###### Replace it with this:
```c#
public class HomeController : Controller
{
    private readonly ISampleService _sampleService;
    
	//private readonly IServiceScopeFactory _serviceScopeFactory;
	private readonly ILifetimeScope _lifetimeScopeFactory; 

    public HomeController(ISampleService sampleService, _lifetimeScopeFactory lifetimeScopeFactory)
    //(...IServiceScopeFactory serviceScopeFactory)
    {
        _sampleService = sampleService;
        //_serviceScopeFactory = serviceScopeFactory;
        _lifetimeScopeFactory = lifetimeScopeFactory;
    }

    [Route("/")]
    public IActionResult Index()
    {
	    //using (IServiceScope scope = _serviceScopeFactory.CreateScope())
	    using (ILifetimeScope scope = _lifetimeScopeFactory.BeginLifetimeScope())
	    {
		   //ISampleService sampleService = scope.ServiceProvider.GetRequiredService<ISampleService>();
		    ISampleService sampleService = scope.Resolve<ISampleService>();
	    }
	    
		return View();
    }
}
```

