---
keywords: show all errors in model
---
Is a collection class that contains all the model state entries. Each entry in the collection corresponds to a property or field in your model. Basically it contains all information about the validation state of that property, validation errors. 

sample:
```c#
//note: this is in a controller
public IActionResult Index(Book book)
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
        return BadRequest(errors); //display error
    }
    return Content($"book ID:{book.bookId} author:{book.author} price:{book.price}", "text/plain");
}
```
The sample above we only used **`ModelState.Values`** for error validation and displaying error message using `Errors`. 
**`ModelState.Values`** is more than that, Below are the properties you can use:

**Errors**: This property is a collection of `ModelError` objects representing validation errors associated with a specific model property. You can access error messages, error codes, and other information from these `ModelError` objects.
```c#
foreach (var entry in ModelState.Values)
{
    foreach (var error in entry.Errors)
    {
        var errorMessage = error.ErrorMessage;
        var errorException = error.Exception;
        var errorCode = error.ErrorCode;
    }
}
```
**RawValue**: This property provides the raw (unconverted) value of the model property as submitted by the client. It can be useful for inspecting the actual value received from a form.
```c#
foreach (var entry in ModelState.Values)
{
    var rawValue = entry.RawValue;
}
```
**AttemptedValue**: This property represents the string value submitted by the client for the model property, as received from the request.
```c#
foreach (var entry in ModelState.Values)
{
    var attemptedValue = entry.AttemptedValue;
}
```
**ValidationState**: This property indicates the validation state for the model property. It can have one of the following values:
- `ModelValidationState.Unvalidated`: The property has not been validated.
- `ModelValidationState.Valid`: The property has been successfully validated.
- `ModelValidationState.Invalid`: The property has validation errors.
```c#
foreach (var entry in ModelState.Values)
{
    var validationState = entry.ValidationState;
}
```
These are some of the commonly used properties of `ModelStateEntry`. You can use them to inspect validation errors, access raw and attempted values, and check the validation state of individual model properties in your ASP.NET Core application.