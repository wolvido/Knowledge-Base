Allows you to create results using methods, so you don't have to write lengthy code.
Sample:
```c#
app.MapGet("/products/{id}", async (HttpContext context, int id) =>
{
	var product = products.FirstOrDefault(p => p.Id == id);
	if (product is null)
	{
		//context.Response.StatusCode = StatusCodes.Status404NotFound;
		//return;
		
		//Instead of doing all that 
		//use IResult instead, much cleaner/better.
		return Results.NotFound(); 
	}
	
	//await context.Response.WriteAsJsonAsync(product);
	return Results.Ok(product); //use this instead of WriteAsJsonAsync
});
```
Another sample:
```c#
app.MapDelete("/products/delete{id}", async (HttpContext context, int id) =>
{
	var existingProduct = products.FirstOrDefault(p => p.Id == id);
	if (existingProduct is null)
	{
		return Results.NotFound();
	}
	products.Remove(existingProduct);
	
	//await context.Response.WriteAsync("Product Deleted");
	return Results.Ok("Product Deleted"); //do this instead of WriteAsync
});
```
#### All `IResult` Implementations:
- `Results.Ok(returnObject)` - Status code 200. Parameter can be string or object. Will return in JSON or text/plain to client.
- `Results.Json(returnObject)` - Status code 200. Parameter must be object. Will only return JSON to client.
- `Results.Text(returnString)` - Status code 200. Parameter must be string. Will only return text/plain to client.
- `Results.File(varies/File)` - Status code 200. Parameter varies. Will only return octet-stream. This is used for file attachments.
	  see: [[FileResult]] for more info. 
	  See [Results.File Method (Microsoft.AspNetCore.Http) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.results.file?view=aspnetcore-8.0) for more details.
###### Error Results
If this is confusing, see [[Status Code Results or Error Results]] for samples.
- `Results.BadRequest(errorResponse)` -  Status code 400. Parameter can be string or object. Will return Object serialized into JSON or text/Plain to client.
- `Results.NotFound(errorResponse)` -  Status code 404. Parameter can be string or object. Will return Object serialized into JSON or text/Plain to client.
- `Results.Unauthorized()` - Status code 401. No parameters. Returns a 401 Unauthorized response to client.
- `Results.ValidationProblem(varies/validationResponse)` - Status code 400. Parameter varies. Returns Dictionary serialized into JSON. See: https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.results.validationproblem?view=aspnetcore-8.0
Sample of `ValidationProblem` use:
```c#
app.MapPost("/create-user", (UserModel user) =>
{
    var modelState = new ModelStateDictionary();

    // Perform some validation
    if (string.IsNullOrWhiteSpace(user.Name))
    {
        modelState.AddModelError("Name", "Name is required.");
    }
    if (user.Age <= 0)
    {
        modelState.AddModelError("Age", "Age must be a positive number.");
    }

    // If there are validation errors, return a validation problem response
    if (!modelState.IsValid)
    {
        return Results.ValidationProblem(modelState);
    }

    // Proceed with normal processing if there are no validation errors
    return Results.Ok("User created successfully.");
});
```
