>[!info]
>This is an excerpt note
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
		return BadRequest(errors); //return BadRequest
	}
	
	//handling logic here if no error exist
	//sample no error return
	return Content($"book ID:{book.BookId} author:{book.Author} price:{book.Price}", "text/plain"); 
}
```