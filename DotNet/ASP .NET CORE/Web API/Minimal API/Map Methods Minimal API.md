Map Methods for creating CRUD Get, Post, Put, and Delete endpoints:
```c#
//`MapGet()`
app.MapGet("/route", async (HttpContxt context) => {
	//...
});
//`MapPost()`
app.MapPost("/route", async (HttpContxt context, Model modelToPost) => {
	//...
});
//`MapPut()`
app.MapPut("/route", async (HttpContxt context, Model modelToPut) => {
	//...
});
//`MapDelete()`
app.MapDelete("/route", async (HttpContxt context) => {
	//...
});
```
# How-To:
- First, assuming we have a model called `Products`:
```c#
public class Product
{
	public int Id {get; set;}
	public string ProductName {get; set;}
}
```
- Then In `Program.cs` add the `Product`:
```c#
List<Product> products =
[
    new Product { Id = 1, ProductName = "Apple" },
    new Product { Id = 2, ProductName = "Banana" }
];
```
==DISCLAIMER==: `products` is just a sample, in real world of course you will use a repository to get products, not to make the objects yourself.
###### `MapGet()`
```c#
app.MapGet("/products", async (HttpContxt context) => 
{
	//await context.Response.WriteAsJsonAsync(products); //Do not use this
	return Results.Ok(products) //use this instead.
});
```
You can also of course implement a specific get:
```c#
app.MapGet("/products/{id}", async (HttpContext context, int id) =>
{
	//get based on Id
	var product = products.FirstOrDefault(p => p.Id == id);
	if (product is null)
	{
		//context.Response.StatusCode = StatusCodes.Status404NotFound;
		//return;
		return Results.NotFound(); //use IResult instead, much cleaner/better.
	}
	
	//await context.Response.WriteAsJsonAsync(product); //Do not use this
	return Results.Ok(products); //use this instead
});
```
###### `MapPost()`
```c#
app.MapPost("/products", async (HttpContext context, Product product) =>
{
    products.Add(product);
    
    //await context.Response.WriteAsJsonAsync(products); //Do not use this
    return Results.Ok(products); //use this instead
});
```
In order to test POST in Minimal API we need to send JSON files, because Minimal API does not support [[form-urlencoded and form-data]].
In order to test it in Postman, use raw and JSON, then manually create a JSON to send:
![[Capture 51.png]]
___
###### `MapPut()`
```c#
app.MapPut("/products/update{id}", async (HttpContext context, int id, Product product) =>
{
	//Finding the product to update using Id
	var existingProduct = products.FirstOrDefault(p => p.Id == id);
	if (existingProduct is null) //if item not found
	{
		//context.Response.StatusCode = StatusCodes.Status404NotFound;
		//return;
		return Results.NotFound(); //use IResult instead, much cleaner/better.
	}
	
	existingProduct.ProductName = product.ProductName; //replace the found product with the product set in the arguments.
	
	//await context.Response.WriteAsJsonAsync(products); //Do not use this
	return Results.Ok(products); //use this instead
});
```
###### `MapDelete()`
```c#
app.MapDelete("/products/delete{id}", async (HttpContext context, int id) =>
{
	var existingProduct = products.FirstOrDefault(p => p.Id == id);
	if (existingProduct is null)
	{
		return Results.NotFound();
	}
	
	products.Remove(existingProduct);
	
	//await context.Response.WriteAsJsonAsync(products); //Do not use this
	return Results.Ok(new { message = "Product Deleted" }); //use this instead
	//or
	return Results.NoContent();
});
```
#### What next?
- Do not use the samples above without [[MapGroups]], the samples above are not DRY. definitely use [[MapGroups]] to DRY the code.
- Don't forget to use [[IResult]] when returning in a Minimal API, because Minimal doesn't know what you are inferring unlike a controller.