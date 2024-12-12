Aside from a testing tool, Swagger is a documentation tool. API needs to be documented of course.
# How-To Document Using Swagger:
###### First is to enable XML documentation file:
1. right click on the project(not the solution)
2. click properties
3. under build, click output and find the checkbox for "Documentation file".
4. Write the xml name or path, sample: "api.xml", this will store the xml in the root, or in a Documentation folder: "Documentation/api.xml"
###### Then in your `Program.cs`, in `AddSwaggerGen(options =>{...})`, include `IncludeXmlComments` with the path of the xml:
```c#
builder.Services.AddSwaggerGen(options =>
{
    options.IncludeXmlComments(Path.Combine(AppContext.BaseDirectory, "api.xml"));
	    //No need to specify the path, it will find "api.xml" wherever it is. As long as the name is correct.
});
```
###### Then in your action method add xml tags `<summary>` , `<return>` and `<param>` if there are parameters:
```c#
/// <summary>
/// says hello to the provided name
/// </summary>
/// <param name="name"> just a name</param>
/// <returns> says hello to the name</returns>
[HttpGet]
[Route("[action]/{name?}")]
public IActionResult GetWithParams([FromRoute] string name)
{
    return Ok($"Hello, {name}!");
}
```
Swagger will automatically show the documentation:
![[screenshot-1715214281287.png]]
>[!warning]
>if you encounter a `Badly formed XML comment ignored for member` error, make sure there's no non breaking spaces in there, manually rewrite the spaces.