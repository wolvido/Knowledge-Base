For returning general-purpose  detailed error information to the client in a standardized format. Usually used for errors in POST or PUT methods of API.
###### Sample:
```c#
[HttpPost]
public IActionResult Create(Product product)
{
    if (product == null)
    {
        var problemDetails = new ProblemDetails
        {
            Title = "Invalid request",
            Status = 400, //400 bad request
            Detail = "Product data is missing or invalid.",
            Type = "https://example.com/errors/bad-request", //optional, will generate automatically if empty
            Instance = HttpContext.Request.Path
        };
        
        return Problem(problemDetails);
    }
    
    // Logic to save the product to the repository
    _repository.Add(product);
    // Return a 201 Created response with the newly created product
    return CreatedAtAction(nameof(GetById), new { id = product.Id }, product);
}
```
#### Parameters:
- Title - Title of the problem.
- Status - status code of the error see [[HTTP status codes]].
- Detail - additional details.
- Type - It's a URI that is used to point to documentation, specifications, or standards related to the problem type. Clients can interpret these URIs to access additional information or context about the problem. It is optional, if its left empty, the type will be automatically generated based on the error.
- Instance - route that led to the error. Optional.