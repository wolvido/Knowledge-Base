Allows to override execution of a specific filter. Preventing the execution of a filter to a specific action method.
For example; you have a filter applied in the [[Class Level Filter]], but you don't want it to execute on one of the action methods.
# How-To:
Actually, there is no such feature in asp net core, only a workaround.
The workaround is simply to create **`SkipFilterAttribute`** and apply the attribute to the action method you want to skip.
Then in your filters, just add an if to return nothing if they detect the **`SkipFilterAttribute`**.
#### File
- Create a `SkipFilterAttribute.cs` in the main Filter folder, or name it however.
#### Syntax:
The Attribute:
```c#
public class SkipFilterAttribute : Attribute, IFilterMetadata
{
	//nothing, this is basically a just a marker.
}
```
---
The Action Method:
```c#
//This is the action method you want the filter to not execute
[SkipFilterAttribute] //simply add the SkipFilterAttribute attribute
public IActionResult SampleActionMethod()
{
	
}
```
---
The Filter:
```c#
public class SampleActionFilter : IActionFilter
{
	public void OnActionExecuting(ActionExecutingContext context)
	{
		//if the current running action method has a SkipFilterAttribute
		if (context.Filters.OfType<SkipFilterAttribute>().Any())
		{
			return; //imeddiately return nothing, essentialllly skipping the filter
		}
	}
	public void OnActionExecuted(ActionExecutingContext context)
	{
	}
}
```
###### Of course this can also work in other filter types not just action filter.
