---
keywords: model class
---
In this note, a model is any data type that is an Entity and POCO. Harsha just calls all POCO as models.
>[!question] Can I add methods in a Model? 
> NO, your model should simply be a [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object), containing as little (if not zero) business logic. A view models only job is to move data from the controller to the view.  
> But you can add a calculated property, so long as this property does not depend on anything outside the model. See [[properties]] for calculated property examples.

A Model represents the structure of data (as properties) that you would like receive from the request as/or send to the response. (Also known as POCO or Plain Old CLR Objects).
- Basically a Model object is the object created from binding the data sent by the front-end, it is the object to be used by the controller, to manipulate and pass to the view.
**For example:**
You have a URL of:
```c#
/bookstore/{price?}?bookId=10&author=winz
```
You can take all the data by using:
```c#
// URL: /bookstore/20?bookId=10&author=winz
[Route("/bookstore/{price?}")]
public IActionResult Index(int price, int bookId, string author)
{
	return Content($"book ID:{bookId} author:{author} price:{price}", "text/plain");
}
```
###### Or you can create a View Model class to combine all the thematically related values into its properties:
```c#
public class Book
{
    public int? bookId { get; set; }
    public int? price { get; set; }
    public string? author { get; set; }
}
```
It becomes the Book Model.
You can then set your action method parameter as Book type:
```c#
// URL: /bookstore/20?bookId=10&author=winz
[Route("/bookstore/{price?}")]
public IActionResult Index(Book book)
{
    return Content($"book ID:{book.bookId} author:{book.author} price:{book.price}", "text/plain");
}
```
==This is called [[Model Binding]].==

So if you wish to specify the source if `FromQuery` or `FromRoute` you set the attributes inside the model:
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
see [[FromQuery and FromRoute]] for more details. 
>[!question]  What if you need to accept multiple `Book` objects or multiple `author` properties? 
>see [[Collection Binding]].
#### Folder Structure:
Models are usually stored in [[Knowledge Base/DotNet/ASP .NET CORE/Services - Service Layer/Entities]], also usually there are no "View Models", the more general term is [[DTO]].

---
### What do I need to know after this?
- In harsha architecture there is no "View Model", the more general term is [[DTO]].
- If you're thinking about adding a function to a model in order to calculate a property, consider just adding a get logic in your property. See: [[properties]].
- Go to [[Model Binding]] to know how view model objects are created through binding.
- Then see [[Collection Binding]] to know how to accept multiple in a request, like multiple `Book` from the sample above.
- Then [[Model Validations]], in order to validate all incoming data to the model. Do not create overly complicated validations in the action method itself. Use Model Validations.
- If you wish to prioritize or specify to take from Query or from Route regardless of the priority order, use [[FromQuery and FromRoute]].
- For security, limit the automatic data bindings accepted by the controller, use [[Bind and BindNever]].
- Finally see [[Strongly Typed Views]] to see how to pass it to views.
Also:
- How do I send data from view to controller? [[form-urlencoded and form-data]].
- For every model or entity, you need to add a ToString() Override, so that when the object is called by a method that expects a string, it returns the string value of the model, not the name of the model itself. see: [[ToString Override]].

