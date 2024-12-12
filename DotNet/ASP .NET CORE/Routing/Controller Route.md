You can add a route to a controller so all action methods use that route like a prefix.
Sample:
```c#
[Route("custom")]
public class YourController : Controller
{
    // This action will be accessible at /custom/details/{id}
    [Route("details/{id}")]
    public IActionResult Details(int id)
    {
        return View();
    }
}
```
### Override
Routes that start with "/" will override the controller route.
sample:
```c#
[Route("custom")]
public class YourController : Controller
{
    // This action will NOT be accessible at /custom/details/{id}
    //it will be accesible at /details/{id} because of the slash at the front
    [Route("/details/{id}")]
    public IActionResult Details(int id)
    {
        return View();
    }
}
```
