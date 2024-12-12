![[Capture 20.png]]
`ContentResult` Syntax:
```c#
public class ContentResult : ActionResult, IStatusCodeActionResult
{
	/// Gets or set the content representing the body of the response.
	public string? Content { get; set;}
	
	/// Gets or sets the Content-Type header for the response,
	/// which may be handled using <see cref="T:Microsoft.Net.Http.Headers.MediaTypeHeaderValue" />.
	public string? ContentType { get; set; }
	
	/// Gets or sets the <see cref="Microsoft.AspNetCore.Http.StatusCodes">HTTP status code</see>.
	public int? StatusCode { get; set; }
	
	//theres also the Task ExecuteResultAsync(ActionContext context), I ommited it, this note is for 
	//functionality
}
```
sample:
```c#
public class SampleController : Controller
{
    [Route("/hello")]
    public IActionResult SampleActionMethod()
    {
        return new ContentResult()
        {
            Content = "Hello from Controller", //the content itself
            ContentType = "text/html" //MIME type
        };
    }
}
```
Or you can just use the Content method provided by ControllerBase:
```c#
public class SampleController : Controller
{
	[Route("/hello")]
	public IActionResult SampleActionMethod()
	{
		//first parameter the content, second parameter overload for content type/MIME type
		return Content("Hello from Controller", "text/plain"); 
	}
}
```
see [[Content()]] method if your confused.