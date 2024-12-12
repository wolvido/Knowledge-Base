This is used in Web API's to return an HTTP 201 (Created) response with a Location header set to the URI of the newly created resource.

This is usually used in POST methods in order for the POST method to return a direct link to to the POSTed data.
#### Sample:
```c#
[HttpPost]
public IActionResult Create(Product product)
{
	_repository.Add(product);
		//adds the new product to the repository
	
	return CreatedAtAction(nameof(GetById), new { id = product.Id }, product);
}
```
`CreatedAtAction` will indicates that the request was successful, and it will include a URL to the newly created resource.
##### `CreatedAtAction` Parameters:
- The first parameter `nameof(GetById)` is the action method that GETSs data, it will be used by `CreatedAtAction` to generate A direct URL to the GET route.
- The `{ id = product.Id }` is needed by the GET method to locate the data in order to provide the correct URL.
- Finally, `product` is passed as the data to include in the response body.
###### The Get Method
```c#
[HttpGet("{id}", Name = nameof(GetById))]
public IActionResult GetById(int id)
{
	var product = _repository.GetById(id);
	if (product == null)
	{
		return NotFound();
	}
	return Ok(product);
}
```

