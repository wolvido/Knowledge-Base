---
keyword: |-
  redirect controller
  redirect action method
---
# RedirectToActionResult
```c#
//only a sample, route values can also carry other values
routeValues = new { redirectRouteValues = currentRouteValues}; 

return RedirectToAction("ActionName", "ControllerName", routeValues) //temporary redirection 302

return RedirectToActionPermanent("ActionName", "ControllerName", routeValues) //permanent redirection 301
```
parameters:
- `"actionName"` - name of the action method. Must be in string.
- `"controllerName"` - Name of the controller where the action method is. Must be in string.
	**NOTE**: the "Controller" in the Controller's name must not be included, if the name is `StoreController`, just put "Store".
- `routeValues` - values that can be passed on to the redirect. It uses anonymous type as input for easier use. see [[Anonymous Types]] if you forgot.
	Sample routeValues use-case:
	- `redirectRouteValues` - the route parameter value to be assigned to the receiving action method.
	- `currentRouteValues` - the current route parameter value from the original link to be assigned to the redirect parameter

The difference between **permanent** and normal is that normal will return a status: 302 for temporary redirection, the permanent will return a 301 for permanent redirection, this is so the client cache will be updated. So use permanent if it is a permanent redirect. see [[HTTP status codes]] for more info.
###### sample:
```c#
public class SampleController : Controller
{
	[Route("Book{idCurrent}")]
	public IActionResult RedirectExample()
	{
		//take the value from the RouteValues Dictionary
		int? idCurrent = Convert.ToInt32(Request.RouteValues["idCurrent"]);
		// Define route values as an anonymous object
		var routeValues = new { idRedirect = idCurrent };
		
		// Redirect to the Details action in the ProductController with route values
		return RedirectToAction("Details", "Product", routeValues);
	}
}
```
**NOTE**: you can also set Route values manually like `var routeValues = new { idRedirect = 200 };`
###### The receiver code of redirection:
```c#
public class ProductController : Controller
{
    [Route("Product{idRedirect}")]
    public IActionResult Details()
    {
        int id = Convert.ToInt32(Request.RouteValues["idRedirect"]);
        // Action logic here
        return Content($"successive {id}", "text/plain");
    }
}
```
##### You can make it mutable by using `nameof`
sample:
```c#
return RedirectToAction(nameof(PersonsController.Index), "ControllerName");
	//dont forget, Controller name needs to be just the name, dont add the Controller
	//instead of "AccountController", just do "Account"
```
This way you don't have to hard code the action method, but controller still needs to be hardcoded.
# LocalRedirectResult
It works the same as `RedirectToAction()` but it uses the route attribute  instead of the action name and the controller name.
Can only be used on local site. Outside site cannot be used. 
**NOTE**: Generally better to use `RedirectToActionResult` since it is more extensible.
sample:
```c#
public class SampleController : Controller
{
	[Route("Book{idCurrent}")]
	public IActionResult RedirectExample()
	{
		int? idCurrent = Convert.ToInt32(Request.RouteValues["idCurrent"]); //take route parameter from RouteValues 
		return LocalRedirect($"store/products{idCurrent}") //returns 302
	}
}
```
**permanent redirect version:**
```c#
	return LocalRedirectPermanents("home/about") //returns 301
	//can also use route parameters like sample above
```
# RedirectResult
Just like `LocalRedirectResult` but not limited to the local web app, can use any url.
**NOTE**: This is rarely used. DO NOT use this for local or just general redirects.
```c#
public class SampleController : Controller
{
	[Route("Product")]
	public IActionResult RedirectExample()
	{ 
		return Redirect("www.google.com/search?q=product") //returns 302
	}
}
```
Also has a permanent redirect version:
```c#
	return RedirectPermanents("www.google.com/search?q=product") //returns 301
	//can also use route parameters like samples above
```