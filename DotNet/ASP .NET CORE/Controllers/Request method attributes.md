You can specify if the action method will only handle post, get, put, etc..
sample:
```c#
public class SampleController : Controller
{
	[HttpGet] //will only receive from a get request, will ignore others
	[Route("/hi")] //url routing is here
    public IActionResult SampleActionMethod()
    {
        return Content("Hello from Controller", "text/plain");
    }
}
```
- `[HttpGet]`: Handles HTTP GET requests.
- `[HttpPost]`: Handles HTTP POST requests.
- `[HttpPut]`: Handles HTTP PUT requests.
- `[HttpDelete]`: Handles HTTP DELETE requests.
- And so on...

The choice of which attribute to use depends on the type of HTTP request your method is intended to handle.
