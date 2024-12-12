To prioritize Query String or Route Data/Parameters input from a model binding route to be used by an action method.
###### For example we have a url of `/bookstore/{bookId}?bookId=10`.
If you set **`FromQuery`**:
```c#
// url: /bookstore/?bookId=10
[Route("/bookstore/{bookId?}")]
public IActionResult Index([FromQuery]int bookId)
{
    return Content($"**bookId:{bookId}**", "text/plain"); //will return bookId:10
}
```
it will output only the query values: **bookId:10**
###### If you set **`FromRoute`**:
```c#
// url: /bookstore/20
[Route("/bookstore/{bookId?}")]
public IActionResult Index([FromRoute]int bookId)
{
    return Content($"**bookId:{bookId}**", "text/plain"); //will return bookId:10
}
```
it will output only the Route values: **bookId:20**

If using a Model Class you can specify it inside the class, sample:
```c#
public class Book
{
	[FromQuery]
	public int? bookId { get; set; }
	[FromQuery]
	public int? price { get; set; }
	[FromRoute]
	public string? author { get; set; }
}
```
see [[Model]] for more detalye.