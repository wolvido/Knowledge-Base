---
keywords: filter order of execution
---
By default, the broader scoped filters will always run sooner than the narrower scoped, but you can create a custom order by setting the Order property.
![[Pasted image 20240304201253.png]]
# How-To:
You can set it in the route of the Filter, sample:
```c#
[TypeFilter(typeof(SampleActionFilter), Order = 1 )]
public async Task<IActionResult> Index()
{
}
```
With arguments:
```c#
[TypeFilter(typeof(SampleActionFilter), Arguments = new object[] {Parameter1, Parameter2}, Order = 1 )]
public IActionResult Index()
{
}
```
##### Note that the order is inversed for **`OnActionExecuting`** and **`OnActionExecuted`**.
So how does the order numbering work?
![[order.png]]
#### `IOrderedFilter`
**`IOrderedFilter`** is another way of setting the order. Also, for [[Global Level Filters]] you cannot set the order using the **`TypeFilter`**.
###### How-To:
In your filter, inherit and implement **`IOrderedFilter`**:
```c#
public class SampleFilter : IActionFilter, IOrderedFilter
{
	public int Order {get; set;} //dont get confused, if you auto implement this it will show a lambda.
	
	//you can hardcode the order in the constructor, or you can have it be accepted as argument
	public SampleFilter(int order)
	{
		//Order = 1; hard coded
		Order = order //or via outside argument
	}
}
```
The argument will be provided in **`TypeFilter`** and for in the **`options.Filters`** for global filters. See [[Filter with arguments]] and [[Global Level Filters]].
sample:
```c#
public class HomeController : Controller
{
	[TypeFilter(typeof(SampleFilter), Arguments = new object[] {order} )] 
	public IActionResult Index()
	{
	}
	//dont get confused, order is a variables with int data
}
```
For the [[Global Level Filters]]:
```c#
builder.Services.AddControllersWithViews(options => {
	options.Filters.Add(new NameOfFilter(order))
});
```
>[!warning] 
>Harsha said that there is a bug with .net; sometimes when using **`IOrderedFilter`**, it instead uses the default order, except for the global filter. Keep that in mind in case there are weird errors in the filters.
