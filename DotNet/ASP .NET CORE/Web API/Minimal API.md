In ASP.Net Core, Minimal API is the new way of doing API. The traditional Controller API uses controllers to map, _Minimal APIs_ define endpoints with logical handlers in lambdas or methods. see: [[Web API]] for Controller API sample.

In Minimal API instead of using controllers, you directly serve it on endpoints, just like [[Middleware]].
###### Sample
Assuming we have the model `WeatherForecast`:
```c#
public class WeatherForecast
{
    public DateOnly Date { get; set; }
    public int TemperatureC { get; set; }
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
    public string? Summary { get; set; }
}
```
We will serve it directly in endpoints:
```c#
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.UseHttpsRedirection();

var summaries = new[]
{
	"Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
};

app.MapGet("/weatherforecast", (HttpContext httpContext) =>
{
	var forecast = Enumerable.Range(1, 5).Select(index =>
		new WeatherForecast
		{
			Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
			TemperatureC = Random.Shared.Next(-20, 55),
			Summary = summaries[Random.Shared.Next(summaries.Length)]
		})
		.ToArray();
	return forecast;
});

app.Run();
```
==No controllers needed.==
##### How to start Minimal API project?
Simply use the "ASP.NET Core Web API " template, but do not check the use controllers.
##### Architecture
You can of course use [[Clean Architecture]] for minimal API. the only difference is no controllers.
##### Minimal vs Web API, what to use?
Use Minimal API if you need ultra fast or ultra simple API's. Web API is much better developer wise.
##### ==Unsupported by Minimal API:==
Minimal API is still young in development, according to microsoft in 8.0 the unsupported features are:
- No built-in support for model binding ([IModelBinderProvider](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.imodelbinderprovider), [IModelBinder](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.imodelbinder)). Support can be added with a custom binding shim.
- No built-in support for validation ([IModelValidator](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.validation.imodelvalidator)). validation needs to be added in [[Endpoint Filters]].
- No support for [application parts](https://learn.microsoft.com/en-us/aspnet/core/mvc/advanced/app-parts?view=aspnetcore-8.0) or the [application model](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/application-model?view=aspnetcore-8.0). There's no way to apply or build your own conventions.
- No built-in view rendering support. We recommend using [Razor Pages](https://learn.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-8.0) for rendering views.
- No support for [JsonPatch](https://www.nuget.org/packages/Microsoft.AspNetCore.JsonPatch/)
- No support for [OData](https://www.nuget.org/packages/Microsoft.AspNetCore.OData/)
# What Next:
- [[Map Methods Minimal API]] - Map Methods for creating CRUD Get, Post, Put, and Delete endpoints for Minimal API.
- Don't forget that you can use [[Route Constraints]].
- [[MapGroups]] - A map group is grouping your endpoints based on their common prefix. This is essentially the Controller of Minimal API. 
- [[IResult]] - When returning in Minimal API, use [[IResult]], because it's not like [[Web API]], Minimal doesn't know what you are inferring unlike a controller.
- [[Endpoint Filters]] - Filters for Minimal API. This is how you implement the model validations.
- [[Minimal API Authentication]] -  Implement authentication and authorization in ASP.NET Core Minimal API.