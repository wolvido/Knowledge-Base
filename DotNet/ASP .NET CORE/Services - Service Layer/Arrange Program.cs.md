---
keywords: |-
  make program.cs cleaner
  separate services in program.cs
  Make IoC cleaner
---
Sooner or later, your `Program.cs` will end up with a lot of registered service and it will be too unwieldy. 
So were gonna need to classify and separate some sections.
# How-To:
We will use [[Extension Methods]]. If you know extension methods, you will already know how to do it.
#### Files
- in your main project, create the folder "StartupExtensions".
- Then, inside the folder, create the file/class `ConfigureServicesExtensions.cs`, this will contain all the service method that will contain the service registrations, or you can name it anything meaningful.
#### Service Extensions
- the class will be static since it will only contain [[Extension Methods]].
```c#
// We will store all the service registration in `ConfigureServicesExtensions` as extensions of `builder.Services`.
public static class ConfigureServicesExtensions
{
	//`builder.Services` is of type `IServiceCollection`, so we will extend `IServiceCollection`
	public static IServiceCollection ConfigureServices(this IServiceCollection services, IConfiguration configuration)
	{
		//then simply copy paste all the service registration from program.cs
		//Instead of `builder.Services...` we will just use `services...` since we already have it as services
		services.AddTransient<ISampleService, SampleService>();
		services.AddScoped<ISampleService, SampleService>();
		services.AddSingleton<ISampleService, SampleService>();
		
		//Then if you have service registrations that uses `builder.Configuration`
		//you can just use `configuration` since we also have `IConfiguration` as argument.
		
		//so instead of this:
		//builder.Services.Configure<SampleModel>(builder.Configuration.GetSection("ConfigParentSample"));
		//you will do this:
		configuration<SampleModel>(configuration.GetSection("ConfigParentSample"));
		
		return services; 
	}
}
```
###### Then register the extension in Program.cs:
simply add:
```c#
builder.Services.ConfigureServices(builder.Configuration);
```
###### Of course you can also create different extension method that have different groups of services, depends on what you need.