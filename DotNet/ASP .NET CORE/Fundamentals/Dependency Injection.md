In most cases you will need to inject classes to other classes, this is how you achieve the [[Dependency Inversion Principle (DIP)]].
#### General method for dependency injection:
1. You have the class that you want to inject:
```c#
public class Service : IService
{
	//...
}
```
2. create its interface:
```c#
public interface IService
{
    //...
}
```
3. implement only the interface to the receiving class and inject the implementation
```c#
public class Injectee
{
	private readonly IService _service;
	
	public Injectee (IService service)
	{
		_service = service;
	}
}
```
This way the service is decoupled and extensible. If you don't know why that is good, see [[Dependency Inversion Principle (DIP)]].
###### Note: that the sample above is the General implementation, it might depend on others.
in ASP.NET you have to register it in the [[IoC]] in `Program.cs`:
```c#
builder.Services.AddTransient<IService, Service>();
```
see: [[Transient, Scoped, Singleton]]