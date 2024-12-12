The View Component Class can supply the View Component view file with View data, just like how the controller can pass view data to the view.
#### Sample:
In the view component controller:
```c#
public class SampleViewComponent : ViewComponent //1
{
	public async Task<IViewComponentResult> InvokeAsync() //2
	{
		ViewBag.Message = "Hello World";
	    return View();
	}
}
```
Then in the view component view file:
```html
<h1>@ViewBag.Message</h1>
```
Any Data can work, not just a hello world string see: [[ViewBag]] for more info.