an action result that represents an object in Javascript Object Notation (JSON) format.
![[Capture 21.png]]
sample:
```c#
namespace Controllers.Controllers
{
	public class SampleController : Controller
	{
		[Route("/helloJson")]
		public IActionResult SampleActionMethod()
		{
			Person person  = new Person() 
			{
				FirstName = "Winz",
				LastName = "Olvido"
			};
			return Json(person); //will return a JsonResult type
		}
	}
}
```
-  to initialize an object first before it can be in JSON
- `Json()` method will convert a c# `JsonResult` type into JSON and return it to the client.
