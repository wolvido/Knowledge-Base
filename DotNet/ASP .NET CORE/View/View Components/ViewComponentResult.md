Return a component view dynamically as needed. just like  [[PartialViewResult]].
# So, How to do it?
The easiest way is to simply create a hidden html section, like for example:
```html
<section class="accounts__overlay accounts__overlay_edit overlay">
    <vc:sample-partial-view></vc:sample-partial-view> //for component views
    //or
    <partial name="~/Views/Shared/sample.cshtml"></partial> //for partial viewa
</section>
```
the in your js, when a button is clicked, simply change the display property no not hidden and it will show.


---
# **Old Method**
The process is basically the same as [[PartialViewResult]] but instead of controller straight to view, its controller to ComponentView handler to view.
### Sample:
So first the controller:
First the controller:
```c#
[Route("list-of-people")]
public IActionResult ListOfPeople()
{
	List<string> ListOfPeople = new List<string>()
	{
		"winzy",
		"jamey",
		"abellina"
	};
	//Obviously you do not create an object in the controller, 
	//it is suppose to be supplied by api or server or the frontend,
	//but for this sample we create it in the controller
	
	//specify the Component View class in the first argument, in this case its name is Sample
	return ViewComponent("Sample", new { employees =  ListOfPeople})
	//in the component view class, there is a parameter called employees
	//so we pass the ListOfPeople as employees in the component view class
}
```
###### Then in the component view class:
```c#
public class SampleViewComponent : ViewComponent
{
	public async Task<IViewComponentResult> InvokeAsync(List employees)
	{
		//Then if we want to add business logic to employees, you can process it here
		
		//in this sample we just send it to the view directly
	    return View(employees);
	    
	    //for view component with custom name you put the model in the second parameter:
	    //return View("_CustomName",sampleModel)
	}
}
```
###### Then create the parent view with the button:
```html
<h1>This is the Parent View</h1>

<button type="button" class="button"> Load the list of employees</button>

//create a container for the component partial view
<section class="list-of-people"> 
	//this will be where the component partial view is injected to
</section>

<script>
	document.querySelector(".button").addEventListener("click", async function(){
		//stores the server response to var response
		var response = await fetch("list-of-people"); // "list-of-people" is the route of the action method
		
		//then reads the response and stores in var listOfPeople
		var listOfPeople = await response.text();
		//it needs to read it first since it is a stream

		//then inject the listOfPeople into its parent view container
		document.querySelector(".list-of-people").innerHTML = listOfPeople;
		//this essentially invokes the partial view into <section class="list-of-people">
	});
//Of course not to mention you should put this script on a separate js
</script>
```

