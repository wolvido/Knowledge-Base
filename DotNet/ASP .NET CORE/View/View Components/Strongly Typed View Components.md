is a component view that is bound to a specified model class.
Basically a [[Strongly Typed Views]] or a [[Strongly Typed PartialView]], but in partial views.
# How?
Works the same as [[Strongly Typed Views]] but instead of passing the object through the controller return, you pass it in the component view class.
sample component view class:
```c#
public class SampleViewComponent : ViewComponent //1
{
	public async Task<IViewComponentResult> InvokeAsync() //2
	{
		SampleModel sampleModel = new SampleModel()
		{
			HelloWorld = "test",
			testInt = 1
		}
		//Obviously you do not hardcode an object in component view class, 
		//it is suppose to be supplied by api or server or the frontend,
		//but for this sample we hardcode it
		
	    return View(sampleModel);
	    
	    //for view component with custom name you put the model in the second parameter:
	    //return View("_CustomName",sampleModel)
	}
}
```
###### Then in the component view, view file, import the model:
```html
@model SampleModel
<h1>@Model.HelloWorld</h2>
<h2>@Model.testInt</h2>
```