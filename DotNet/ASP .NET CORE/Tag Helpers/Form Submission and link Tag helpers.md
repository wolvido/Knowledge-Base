---
keywords: tag helper route parameter
---
Allows you to specify which controller and action method the tag sends data to dynamically without specifying the url.
>[!question] Why? What is the advantage? What is its purpose?
> 1. Separation of concerns/encapsulation - When creating links in the view using Tag Helpers, the developer specifies the controller and action without worrying about the details of routing configuration. The framework takes care of generating the correct URLs based on the routes configured in the controllers.
> 2. Polymorphism - You can dynamically change where the form sends data.
###### Sample:
instead of:
```html
<form action="/route/to/action">
	...
</form>
```
You can do:
```html
<form asp-controller="controller-name" asp-action="action-method-name">
	<input type="submit" />
</form>
```
Will automatically generate the action link.
This way you can easily point to where controller and action method the data is sent to without changing the link and you can dynamically change it.
Also it separates the concern since the view doesn't need to know the routing configuration.
>[!tip]
>Also when creating forms, use [[Input and label tag helpers]]
- Also works on hyperlinks:
```html
<a asp-controller="controller-name" asp-action="action-method-name"> //no need for href
	...
</a>
```
- Also works on the submit button of the form, instead of the tag helper on the form itself:
```html
<form method="post">
    <button asp-controller="Home" asp-action="Index">Click Me</button>
    //or
    <input asp-controller="Home" asp-action="Index">
</form>
```

>[!warning]
>make sure the "controller-name" does not include the Controller post fix, just the name.
#### What If your form has two submit buttons
For example you have a form with submit button and a delete button:
```html
<form method="post">
	<button asp-controller="Home" asp-action="Delete">Click Me</button> 
	//or
	<input type="image" asp-controller="Home" asp-action="Submit"> 
</form>
```
#### What if the action method route needs a route parameter?
you add `asp-route-nameOfRouteParameter`.
for example:
let say you have this action method in the `Home` controller that accepts a route parameter:
```c#
[Route("[controller]")]
public class HomeController : Controller
{
	[Route("[action]/{dataToUpdate}")]
	public IActionResult Update(DataTypeSample dataToUpdate)
	{
	    //code that updates the database etc...
	}
}
```
You can refer to it by using:
```html
<a asp-controller="Home" asp-action="Update" asp-route-dataToUpdate=1234>Link Text</a>
// this does not work on buttons, only links.
```
Essentially will route to
```c#
Home/Update/1234
```
and will register the route parameter data.
###### You can also pass model data of course.
for example:
```html
<a asp-controller="Home" asp-action="Update" asp-route-dataToUpdate="@Model.SampleId.Id">Link Text</a>
<form asp-controller="Home" asp-action="Update" asp-route-dataToUpdate="@Model.SampleId.Id">
	...
</form>
```
[[Model Binding]] will automatically receive the data.
#### Questions:
- if the form has a `asp-controller="controller-name" asp-action="action-method-name"` but the submit button inside the form also has its own `<input asp-controller="Home" asp-action="Submit">` what will happen?
	- whichever input is pressed will take precedence, so if `<input asp-controller="Home" asp-action="Submit">` is pressed, then this will take precedence.
	- If an input with submit type but no route is pressed, then the route in the form will take precedence.