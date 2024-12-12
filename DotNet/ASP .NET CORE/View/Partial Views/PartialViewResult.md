Return a partial view dynamically/lazy loaded in a press of a button or something else.
#### Without Input Partial View
- For example, you have a site that needs to show a List of People when a button is pressed, and the list of people needs to be loaded from the back.
- So the way you would do this is to create a partial view for the list of people, then you invoke that partial view to the normal view that has that button.
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
	
	//specify the partial view in the first argument
	return PartialView("_PeoplesPartialView", ListOfPeople)
	//add the object name in the second argument
}
```
###### Then create the parent view with the button:
```html
<h1>This is the Parent View</h1>

<button type="button" class="button"> Load the list of people</button>

//create a container for the partial view
<section class="list-of-people"> 
	//this will be where the partial view is injected to
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
This way whenever `<button type="button">` is pressed, the partial view will be asynchronously loaded into the parent view.
>[!info]
>This is not the only way to dynamically use PartialViewResult, you can also use some razor scripts that invoke a partial view dynamically depending on the requirements.
---
>[!info]
>`response.text()` only reads text or html. if your return type is of json it needs to be `response.json()` and other response types have their own also, just look it up.
#### With Input and with JQuery
If you need to dynamically load a partial view result that has parameters.
###### First your html needs to have data attribute to pass to js:
```html
<button data-dataToPass="dataToPass" ></button>
```
###### Set up the container for your partial view result
```html
<section class="container">

</section>
```
###### Set up the action Method
```c#
[Route("[action]/{dataToPass}")]
[HttpGet]
public async Task<IActionResult> ActionMethod(string dataToPass)
{
	//process the data...
	SampleModel = SampleMethod(dataToPass);
	
    return PartialView("~/path/to/partialView.cshtml", SampleModel);
	    //Sample Model is the strogly typed model on partial view to pass to
}
```
###### The in Js
```js
$("button").on("click", async function () {
        var accountId = this.getAttribute('data-dataToPass');

        //fetch and apply the partial view
        var response = await fetch(`/ActionMethod/${accountId}`); //fetch the data 
        var updateAccountData = await response.text();
        $(".container").html(updateAccountData); //add partial view to the cotainer

        //reset form validation
        $(".accounts__overlay_modify form").data("validator", null);
        $.validator.unobtrusive.parse(".accounts__overlay_modify form");
	        //If you are using tag helpers, the validation will be removed, so it needs to be reset.
    });
```
>[!warning]
>If somehow you have two action methods with the same name, but one is for GET partial view while the other is POST, it might return an error. 
>see: [[Cannot read properties of null (reading 'classList')]]
___
>[!warning]
> On tag helper validation, only `<div asp-validation-summary="All"></div>` will work, if we use this method.
> `asp-validation-for` will not work.