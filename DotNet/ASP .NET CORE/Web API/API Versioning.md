Sometimes some clients have not updated yet and will still need to use older version of your API, that's why you need the ability to serve different versions of an API/Service. 
![[Pasted image 20240509094818.png]]
[[Swagger]] will need to be used.
# How-To:
Api versioning needs to have a system for reading the version, because Client applications consuming the API need to know which version of the API they are interacting with. 
There are three ways of version reading: `UrlSegmentApiVersionReader`, `QueryStringApiVersionReader`, and `HeaderApiVersionReader`,
- But first, nuget install `Asp.Versioning.Mvc` **and** `Asp.Versioning.Mvc.ApiExplorer`.
#### `UrlSegmentApiVersionReader`:
- enable `UrlSegmentApiVersionReader` versioning , in your `Program.cs`: 
```c#
builder.Services.AddApiVersioning(config =>
{
	config.ApiVersionReader = new UrlSegmentApiVersionReader(); 
		//includes the version number in the URL `api/v1/sample`
})
	.AddMvc(); //make sure to add .AddMvc()
```
==Make sure `Services.AddApiVersioning()` is below `Services.AddControllers`== or any variation of `AddControllers`.
###### Folder Structure
- let's say you have v1 controllers, and v2 controllers, so in your "Controllers" folder, create a "v1" folder and a "v2". Move all your controllers to their respective folder versions.
- Then on the controller route, you need to set the versions dynamically, sample:
```c#
[Route("api/v{version:apiVersion}/[controller]")]
public class SampleController : ControllerBase
{
	//...
}
```
can also be applied on [[Custom ControllerBase]] for DRY.
- Then also on your controllers, explicitly specify the version where the controller belongs:
```c#
[ApiVersion("1.0")] //can also specify minor version like [ApiVersion("1.2")] 
public class SampleController : ControllerBase
{
	//...
}
```
So now if you run this URL: `api/v1/Sample`, it will run Sample Controller version 1 only.
#### `QueryStringApiVersionReader`
in your `Program.cs` use 
```c#
builder.Services.AddApiVersioning(config =>
{
	config.ApiVersionReader = new QueryStringApiVersionReader();
		//reads the version in the query string `api/sample?api-version=1.0`
	
	config.DefaultApiVersion = new ApiVersion(1, 0);
	config.AssumeDefaultVersionWhenUnspecified = true;
		//If the client does not specify the version, then it will assume to use the default version 1.0
})
	.AddMvc(); //make sure to add .AddMvc();
```
###### How it works?
When using `QueryStringApiVersionReader`, you don't need to add the version in the route itself, the client will specify the version by adding a query string. 
For example, if the client wants v1, then by default he sends a request with the URL: `api/sample?api-version=1.0` or `api/sample?api-version=2.0`. If the client does not specify the version, then it will assume to use the set default version.
==Folder Structure would work the same way as above==
#### `HeaderApiVersionReader`
```c#
builder.Services.AddApiVersioning(config =>
{
	config.ApiVersionReader = new HeaderApiVersionReader("api-version");
		//reads version number from request header, sample: `api-version: 1.0`
		
	config.DefaultApiVersion = new ApiVersion(1, 0);
	config.AssumeDefaultVersionWhenUnspecified = true;
		//If the client does not specify the version, then it will assume to use the default version 1.0
})
	.AddMvc(); //make sure to add .AddMvc();
```
###### How it works?
The version needs to be added in the header. For example:
![[Screenshot 2024-05-11 at 12-27-14 Asp.Net Core 8 (.NET 8) True Ultimate Guide.png]]
If version number is not added, then as long as you set `DefaultApiVersion` and `AssumeDefaultVersionWhenUnspecified`, it will assume default version.
==Folder Structure would work the same way as above==
###### **Which one to use?**
Depends, usually `UrlSegmentApiVersionReader` is used since it is flexible and easy to use, simply add it in the URL.
#### What Next?
- Versioning will now work, but it will still run an error for swagger, you need to [[Enable API Versioning in Swagger]].
