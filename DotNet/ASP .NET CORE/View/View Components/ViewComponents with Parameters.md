Being able to pass data from the view to the component view handler. 
# How?
In your invoking view, you add the parameters depending on how it was invoked.
sample:
```c#
<h1>Home</h1>
@{ //sample object to be sent as parameter
	SampleObject sampleObject = new SampleObject()
	{
		testProperty = "test",
		testProperty2 = 123
	}
}

//the invoking code
@await Component.InvokeAsync("Grid", new {
	samplePassString= "sample",
	samplePassInt = 1234,
	samplePassAnObject = sampleObject //here we pass the object we made above
})
```
You can also pass it using the tag helper method:
```html
<vc:name-of-view-component parameter1="value1" parameter2="value2"></vc:name-of-view-component>
//`parameter1` must match the name of the parameter in the view component class
//"value1" string must match the name of a variable in the view
```

Then in the view component handler class:
```c#
public class SampleViewComponent : ViewComponent 
{
	public async Task<IViewComponentResult> InvokeAsync(string samplePassString, int samplePassInt, SampleObject sampleObject) //here you receive the parameters
	{
		//manipulate the parameters here and pass the results depending in whats needed
		//here is a sample process:
		if(sampleObject.testProperty == null)
		{
			sampleObject.testProperty = samplePassString;
		}
		if(sampleObject.testProperty2 == null)
		{
			sampleObject.testProperty2 = samplePassInt;
		}
	    return View(sampleObject); //returns the processed object to a strongly typed component view
	    //If you have a custom name for the view, then you should:
	    //return View("_NameOfTheView", sampleObject); 
	}
}
```