Easily generate the selections of the `<select>` dropdown tab and also be able to dynamically generate it.
# How-to:
lets say you have this model:
```c#
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
}

public class MyViewModel
{
    public int SelectedProductId { get; set; }
    public List<Product> ProductList { get; set; }
}
```
And you want to create a `<select>`dropdown using the `ProductList` property.
In your controller:
```c#
public IActionResult Index()
{
	// data is hardcoded for sample sake, in real world its not hardcoded
    var model = new MyViewModel;
    model.ProductList = new List<Product>
	{
		new Product { Id = 1, Name = "Product A" },
		new Product { Id = 2, Name = "Product B" },
		new Product { Id = 3, Name = "Product C" }
	}
    
    return View(model);
}
```
In the view:
```html
<!-- Using asp-items with a <select> element -->
<form>
    <label for="selectedProductId">Select a product:</label>
    <select asp-for="SelectedProductId" asp-items="@Model.ProductList"></select>
    <button type="submit">Submit</button>
</form>
```

This is just one implementation, there are many other depending on your code, see: https://stackoverflow.com/a/34624217/13107848 for a really comprehensive answer.