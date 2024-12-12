When making a controller for an API you need to add `[ApiController]` attribute, you need to add the `[Route("api/[controller]")]`, and you also have to inherit from `ControllerBase`, and also sometimes you might have basic crud methods that you don't want to repeat to all controllers.
But you can combine all that in a custom controller base class, and have that class be inherited.
# How-To:
```c#
//apply all the attribute and route to the custom class
[Route("api/[controller]")]
[ApiController]
public class CustomControllerBase : ControllerBase // and also inherit from ControllerBase
{
	//add the basic methods
	[HttpGet("{Id}")]
	public async Task<IActionResult> Get()
	{
	    //a universal get, maybe all your application needs a get that gets the same thing
	}
}
```
That's it, now you can just apply `CustomControllerBase` on you controllers:
```c#
//no need for [ApiController] and [Route("api/[controller]")]
public class PracticeController : CustomControllerBase
{
	//no need to add the universal get, its already there.
}
```