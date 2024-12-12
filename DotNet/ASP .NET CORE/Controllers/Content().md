syntax:
```c#
Content(String) //Creates a content result object by using a string.
```
Overloads:
```c#
Content(String, String) //Creates a content result object by using a string and the content type.
Content(String, String, Encoding) //Creates a content result object by using a string, the content type, and content encoding.
```

Basically Its an easier way of creating a `ContentResult` type for the action method. See [[Content Result]] for more detalye
Sample:
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
Instead of doing the sample above,  you can use:
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
There are various type of MIME types, see [[What is Content type-MIME type]].
You can also use `text/html`:
```c#
public class SampleController : Controller
{
	[Route("/hello")]
	public IActionResult SampleActionMethod()
	{
		//first parameter the content, second parameter overload for content type/MIME type
		return Content("<h1>Hello from Controller</h1>", "text/html"); 
	}
}
```
