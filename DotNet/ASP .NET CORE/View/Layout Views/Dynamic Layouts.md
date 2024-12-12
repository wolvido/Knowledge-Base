As the title suggests, it is dynamic layouts that change, because not all pages can always have the same layout, sometimes you need a different layout view for certain user actions.
>[!info]-
>Read [[_ViewStart.cshtml]] first for context of this.
---
>[!info]
> If you dont need to swap layout, if you just want to add extra elements on a view, you should use [[Partial Views]].
### How to do it?
You can do it by using [[ViewBag]]s

For example, you have an e-commerce site with a default layout, but if the user wants to search for a product you need to have a search layout instead of a default.
You set up a controller to pass search data using viewbag:
```c#
[Route("product-search/{ProductId}")]
public IActionResult Search(int ProductId)
{
	ViewBag.ProductId = ProductId;
	return View();
}
```
Then in that view, you set a layout by condition or any other way to set a layout dynamically:
```html
{
	if (ViewBag.ProductId != null)
	{
		Layout = "~/Views/Shared/_ForSearchingLayout.cshtml" //setting a layout will override ViewStart Layout
	}
}
<h1>Search Products</h1>
//code etc..
```
The default layout set will override the View Start layout, but the View Start Layout will still apply if  **`ProductId`** is null. Making it dynamic.
>[!warning]
>a view can only have one layout
---
>[!question] 
>###### What if I don't want whole layouts to dynamically change, what if I only need a section of a layout to change. 
>You use [[Section Layout Views]].
---
>[!info]
> If you dont need to swap layout, if you just want to add extra elements on a view, you should use [[Partial Views]].
