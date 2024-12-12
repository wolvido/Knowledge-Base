A map group is grouping your endpoints based on their common prefix. It helps DRY code.
It's essentially the Controller of Minimal API.
So for example route:
```c#
"/products/get"
"/products/post"
"/products/delete"
```
All belong to:
```c#
var ProductmapGroup = app.MapGroup("/products");

mapGroupProduct.MapGet(...);
mapGroupProduct.MapPost(...);
```
# How-To:
First register the Map Group in `Program.cs`:
```c#
var mapGroupProduct = app.MapGroup("/products");
```
Then for your endpoints, instead of doing this:
```c#
app.MapGet("/products/{id}", async (HttpContext context, int id) =>
{
	//codes...
});
```
==You can just do this==:
```c#
ProductmapGroup.MapGet("/{id}", async (HttpContext context, int id) =>
{
	//codes...
});
```
So you don't need to repeat code, it makes the code DRY.
#### Separate the `MapGroup`
The sample above still assumes that the map methods are all in `Program.cs` which means it still no grouped enough. We need to separate the map methods on its own folder and class, just like how you would in a controller.
###### 1. First, create a new folder called "RouteGroups", If you are using [[Clean Architecture]] or N-tier "RouteGroups" is essentially the Controller folder.
###### 2. Inside "RouteGroups" create a class called `"<nameOfMapGroup>sMapGroup.cs"` like for example: "ProductsMapGroup.cs".
###### 3. Inside the class create an [[Extension Methods]] and the Data source. Sample:
```c#
public static class ProductsMapGroup //note that ProductsMapGroup is just a sample, it could be "EmployeesMapGroup" etc...
{
	//Data source field
	private static List<Product> products =
	[
	    new Product { Id = 1, ProductName = "Apple" },
	    new Product { Id = 2, ProductName = "Banana" }
	];
	//DISCLAIMER: `products` is just a sample Data source, in real world of course you inject a repository or a service to this Controller/MapGroup. Assuming you know how to inject a service or repo.
	
	//create the extension method to inject to the map group
	public static RouteGroupBuilder ProductsAPI(this RouteGroupBuilder group) //"ProductsAPI" name is just a sample name
	{
		//Here you will put all the Map methods
		group.MapGet("/route", async (HttpContxt context) => {
			//...
		})
		//`MapPost()`
		group.MapPost("/route", async (HttpContxt context, Model modelToPost) => {
			//...
		})
		//`MapPut()`
		group.MapPut("/route", async (HttpContxt context, Model modelToPut) => {
			//...
		})
		//`MapDelete()`
		group.MapDelete("/route", async (HttpContxt context) => {
			//...
		})
		
		//You will use "group.MapGet" instead of "ProductmapGroup.MapGet", it will refer to the same thing.
		
		return group;
	}
}
```
###### 4. Then in your `Program.cs`, simply inject into the MapGroup:
```c#
var mapGroupProduct = app.MapGroup("/products").ProductsAPI(); //inject ProductsAPI here
```
If you have endpoints in `Program.cs`, copy paste them into your extension method. This way `Program.cs` stays very clean and the endpoints get grouped in separate files.
