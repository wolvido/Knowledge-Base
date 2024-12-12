Attributes to apply in action methods to specify the request method. see: [[HTTP request methods]]
- `[HttpGet]`
- `[HttpPost]`
- `[HttpPut]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpPatch]`
Sample:
```c#
using Microsoft.AspNetCore.Mvc;

namespace YourNamespace.Controllers
{
    public class SampleController : Controller
    {
        // GET: /Sample/Form
        [HttpGet]
        public IActionResult Form()
        {
            // This action method is for accessing the form page (GET) 
            // so that it doesn't submit the form when opening the page
            return View();
        }

        // POST: /Sample/Form
        [HttpPost]
        public IActionResult Form(string formData)
        {
	        // This action method is when the form is submitted for (POST) 
	        
	        // Process formData here...
        }
    }
}
```