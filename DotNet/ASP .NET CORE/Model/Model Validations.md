![[Capture 23.png]]
###### Instead of creating validations on the action method like:
```c#
public IActionResult Index(Book book)
{
	if (book.bookId != null) //validate if BookId is not null
	{
		return Content($"book ID:{book.bookId} author:{book.author} price:{book.price}", "text/plain");
	}
}
```
###### You should instead do this to your model class:
```c#
public class Book
{
	[Required] //BookId is required, will throw error if null
	public int? BookId { get; set; }
	public int? Price { get; set; }
	public string? Author { get; set; }
}
```
will throw an error if **bookId** is null.
>[!question] how does it work?
 if a Model Validation is not met, it will register an error.
##### So how do we handle the error if a validation is triggered?
see: [[Model validation error handling]]

>[!info] 
Of course `[Required]` is not the only validation attribute, there are various model validation attributes for the complete list see: [[Model Validations Attributes]]
you can also create a custom model validation, see: [[Custom Model Validation Attribute]]