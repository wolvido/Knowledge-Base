For example, you have this model:
```c#
public class Book
{
	[Required] //BookId is required, will throw error if null
	public int? BookId { get; set; }
	public int? Price { get; set; }
	public string? Author { get; set; }
}
```
If **BookId** is null, the error will be stored in the **Model State** dictionary and properties (these are properties of Controller). You will handle the Model States in the controller action method.

To check if validation errors exist we use **Model States**:
#### Model States
**IsValid**: Specifies whether there is one validation error or not. (Boolean type)
```c#
public IActionResult Index(Book book)
{
	if (!ModelState.IsValid) //validate if error does not exist
	{ // if it does exist
		//handle the validation error
	}
}
```
#### Handling validation error
If validation errors exist, To handle the errors, generally you can show the validation warnings to the user using [[Client Side Validations tag helpers]].

**ErrorCount**: Returns the number of errors.
```c#
public IActionResult Index(Book book)
{
	if (ModelState.ErrorCount > 0) 
	{
		return BadRequest("errors exist);
	}
	return Content($"book ID:{book.BookId} author:{book.Author} price:{book.Price}", "text/plain");
}
```

**Values**: It is a collection class that contains all the model state entries. Each entry in the collection corresponds to a property or field in your model. Basically it contains all information about the state of that property, including any validation errors, thats why it can be used for error validation.
Sample:
```c#
public IActionResult Index(Book book) //book is the sample model, any model can work
{
	List<string> errorList = new List<string>();
	foreach (var entry in ModelState.Values) //ModelState.Values is a Collection Class
	{
		foreach (var error in entry.Errors) //for every entry there is also a collection of Errors
		{
			var errorMessage = error.ErrorMessage; //convert error to string
			errorList.Add(errorMessage); //add all errors to a list
		}
	}
	string errors = string.Join("\n", errorList); //combine all and display per line
	
	if (!ModelState.IsValid) //validation if error exists
	{
		//error handling logic here if error exist
		return BadRequest(errors); //return BadRequest if they exist
	}
	
	//handling logic here if no error exist
	//sample no error return
	return Content($"book ID:{book.BookId} author:{book.Author} price:{book.Price}", "text/plain");
}
```
**NOTE:** The sample above, we only used **`ModelState.Values`** to take the error message, but it is more than that, **`ModelState.Values`** is not only used for error handling. See [[ModelState.Values]] for more info.
##### Custom Error Message
You can also add a custom error message to the **`ModelStateEntry`** Collection.
Sample:
```c#
public class Book
{
	[Required(ErrorMessage = "BooK ID cannot be empty or null")] //this will be displayed in Status Code Results
	public int? BookId { get; set; }
	public int? Price { get; set; }
	public string? Author { get; set; }
}
```
you can also add the property name in the message:
```c#
public class Book
{
    [Required(ErrorMessage = "{0} cannot be empty or null")] //will return "BookId cannot be empty or null"
    public int? BookId { get; set; }
    [Required(ErrorMessage = "{0} cannot be empty or null")] //will return "Price cannot be empty or null"
    public int? Price { get; set; }
    public string? Author { get; set; }
}
```
can only be set to `{0}` since there is only one value set in this attribute.

**But what if you don't want the display name to be `bookId` but instead Book ID**.
You set the **`[Display]`** attribute
```c#
public class Book
{
	[Display(Name = "Book ID")] //display name is set to Book ID instead of bookId
    [Required(ErrorMessage = "{0} cannot be empty or null")] //will return "Book ID cannot be empty or null"
    public int? BookId { get; set; }
    [Required(ErrorMessage = "{0} cannot be empty or null")] //will return "Price cannot be empty or null"
    public int? Price { get; set; }
    public string? Author { get; set; }
}
```
**NOTE:** Display is not a Validation Attribute, It is a Different kind of beast altogether, with its own different properties.
In this example, the `[Display]` attribute is used to specify how the properties should be labeled in a user interface.
> [!tip]
>**If None of these attributes work**, create your own, see [[Custom Model Validation Attribute]].

