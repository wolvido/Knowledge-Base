A web API is a [[View]]less service, that is used by other applications. Sample is the [Weather API - OpenWeatherMap](https://openweathermap.org/api), you can use it to get data on the current weather. These are the things that return json or xml when called.
ASP .NET Web API is part of .NET Core which is used to create API's.
#### RESTful
[[RESTful]] API is an architectural style that defines the creation of HTTP services that receive [[HTTP request methods]], perform CRUD, and returns json or xml response to the client.
![[Pasted image 20240502050826.png]]
Read [[RESTful]] first, before going in.
# How-To:
- We can start the project by using the built in template "ASP.NET CORE Web API" in visual studio.
- Naming convention is to suffix the project name with ".WebAPI". Also in the solution name, remove the ".WebAPI" and just change it to "Solution".
- Then in this sample we will check "use controllers", we will not use [[Minimal API]], it is a separate section; separate learning.
- Leave Open API unchecked, [[Swagger]]/Open API is in a separate section.
- Leave top-level statements unchecked. We will use top-level statements for the `Program.cs`, it's the same as you're used to.
Don't be surprised or confused, its still .NET, everything is the same, the only difference is there is no views. What works on previous .NET programs, will work here. The only thing that will not work is the views.
It's also advisable to configure [[HTTPS]].
#### Web API Controllers
The controllers in a Web API is exactly the same, except it inherits from `ControllerBase` and it has the `[ApiController]` Attribute, but functionally its the same. returns json or xml instead of view.
>[!question]- Why `ControllerBase`?
> Because `Controller` is specially made for MVC and Views. `ControllerBase` was later made to be the base for non MVC controllers, like API controllers.
###### When adding controllers, make sure you choose the **API controller** in the template selection, not the **MVC controller**.
Sample:
```c#
[Route("api/[controller]")] 
	//adding "api/" as pre-fix for api controller route is a common practice but not a standard
[ApiController]
public class PracticeController : ControllerBase
{
	[HttpGet] //always use 
	public IActionResult Get()
	{
		return Ok("Hello World!");
			//Ok method is returns a json response with status code 200 to indicate request successfull.
	}
	
	[HttpGet]
	[Route("[action]/{name?}")]
	public IActionResult GetWithParams([FromRoute] string name)
	{
		return Ok($"Hello, {name}!");
	}
}
```
###### What does `[ApiController]` do?
It automates and enforces various things specific to API's, for example you don't need to add [[FromBody]] since it's already understood that an API uses JSON or XML.
It also automatically returns an object as a json format, for example:
```c#
[HttpGet("{sample}")]
public async Task<ActionResult<Sample>> GetSamplebById(string Id)
{
	var Sample sample = //accessing service...
	
	return sample;
		//will automatically return the Json equivalent of the Sample model.
}
```
##### launchSettings
By default of the template, the Launch URL is going to be: "weatherforecast", you need to change it, open `launchSettings.json` and change it to **"api/nameOfController"** or if using the sample above **"api/Practice"**.
##### Clean Architecture
Of course, Web API can also follow [[Clean Architecture]].
# What next?
- [[EFCore Web API]] - explains itself.
- [[CreatedAtActionResult()]] - use this as a return for a POST method. You can refer to [[IActionResult]] for everything else.
- [[Web API Request Methods]] - Most common way to create Web API Request Methods and some guidelines.
- For security, limit the automatic data bindings accepted by the controller, use [[Bind and BindNever]].
- [[Custom ControllerBase]] - to further DRY the code, and implement common basic CRUD methods
- [[Swagger]] - To easily test and document your API. This is very useful.
- [[Content Negotiation API]] - read [[Content Negotiation]], now this note is for specifying what mime type should the API produce or consume.
- [[API Versioning]] - Sometimes some clients have not updated yet and will still need to use older version of your API, that's why you need the ability to serve different versions of an API/Service.
#### ==Minimal API==
Use Minimal API if you need ultra fast or ultra simple API's. [[Minimal API]].