---
keywords: |-
  routing with the same name 
  controller name on route
  action name method on route
---
Instead of having to manually creating route paths, you can use route attributes to set it to the name of the action method or controller. You can also specify what verb requests the route will accept.
sample:
```c#
[Route("api/[controller]")]
public class ProductsController : Controller
{
    // This action responds to GET requests at /api/products/GetProducts
    [Route("[action]")]
    public IActionResult GetProducts()
    {
        // Your action logic
        return Ok("List of products");
    }

    // This action responds to GET requests at /api/products/{id}
    [HttpGet("{id}")]
    public IActionResult GetProduct(int id)
    {
        // Your action logic
        return Ok($"Product with ID {id}");
    }

    // Other routes and actions such as [HttpPut("{id}")] or [HttpPost] etc...
}
```
#### All Verb Requests:
- `[HttpGet]`
- `[HttpPost]`
- `[HttpPut]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpPatch]`