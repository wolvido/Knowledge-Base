Basically the same as [[Strongly Typed Views]] but you call a Parent Model/Wrapper Model that contains the multiple models you need.
# How It Works:
**The Models:**
```c#
namespace YourNamespace
{
	public class User
	{
	    public int? Id { get; set; }
	    public string? Name { get; set; }
	    public string? Email { get; set; }
	}
	
	public class Product
	{
	    public string? Name { get; set; }
	    public string? Category { get; set; }
	    public string? Description { get; set; }
	}
	
	public class Order //this is the wrapper/parent
	{
	    public User? User { get; set; }
	    public Product? Product { get; set; }
	}
}
```
>[!info]
>In the real world every model is a separate file not combined like the sample above.

**The Controller:**
```c#
public class HomeController : Controller
{
    [Route("/")]
    public IActionResult Index(Order? order) //we will use auto model binding
    {
        return View(order);
    }
}
```
We used model binding to accept and create the order object, but in order to not confuse the model binding on properties of the same name from the two models, we have to specify it like so:
![[Capture 30.png]]
So it will not confuse property Name, since Product and User has both property Name.
**The View**
```html
@using View.Models
@model Order
<!DOCTYPE html>
 
<html>
<body>
<h1>Home</h1>
<h2>user: @Model.User.Name</h2>
<h2>user ID: @Model.User.Id</h2>
<h2>user Email: @Model.User.Email</h2>
 
<h2>Product: @Model.Product.Name</h2>
<h2>Product Category: @Model.Product.Category</h2>
<h2>Product Price: @Model.Product.Description</h2>
</body>
</html>
```
So if the query string is: **`?User.Id=2&User.Name=winz&User.Email=best email&Product.Name=IPhone&Product.Category=pricey&Product.Description=very pricey`**
The output will be:
![[Capture 31.png]]