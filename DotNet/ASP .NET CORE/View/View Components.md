>[!warning]
>View Components and partial views cannot use `@section` and implement its own unique js script and css style.
>
>If you really need to theres a workaround, but if you are using jquery and other libraries, it will be loaded twice. workaround: https://github.com/aspnet/Mvc/issues/2910#issuecomment-356276338
>
>The workaround is to essentially create a special `_Layout` for partial views that has its own [[Section Layout Views]], then apply the layout to the partial views.
>There's also another workaround where you use inline javascript to import the external javascript.

Basically partial views, but capable of handling complex server side logic. Partial views cannot do server-side logic, the controller should not do logic for a partial view. Instead, you use a View Component. see [[Partial Views]] for detalye.
This is used for self-contained views that can be placed anywhere, the view component must have input, otherwise it is a partial view.
## How to View Component?
#### First Program.cs
make sure to add:
```c#
builder.Services.AddControllersWithViews();
app.UseStaticFiles();//if you plan to add static files to your View Component
app.UseRouting();
app.MapControllers();
```
#### Folder structure
- Create a "ViewComponents" folder just like the controller folder. This is where the View Component classes are stored.
- Then the Partial Views of the Component views is by default stored in "Views/Shared/Components/**NameOfTheClass**/Default.cshtml",  **NameOfTheClass** is the name of the Component View class that handles the component view cshtml file.
	So for example: you have a view component class of `SampleViewComponent.cs` so the file path for your view files would be "Views/Shared/Components/**NameOfTheClass**/Default.cshtml"
#### Naming
The name of the view .cshtml file of component views is by default "Default.cshtml".
>[!info]
>if by chance you want a different name, then you need to mention it specifically in the `return View("NameOfTheViewFile")`.

View Component class file name must add "ViewComponent" to their last name, for example: "SampleViewComponent.cs"
>[!info]
>If by chance you do not want to add "ViewComponent" to the last name, then you must add the `[ViewComponent]` attribute to the class. Not advisable though.
#### Create the view component class:
Create a ViewComponent class in the "ViewComponent" folder. 
1. The class should inherit from `ViewComponent`.
2. Add an async `InvokeAsync()` with a return type of `Task<IViewComponentResult>`.
Sample:
```c#
public class SampleViewComponent : ViewComponent //1
{
	public async Task<IViewComponentResult> InvokeAsync() //2
	{
		//Put the logic here
	    return View();
	}
}
```
#### So how to invoke the view component to a parent view?
By adding: `@await Component.InvokeAsync("NameOfTheComponentClass")`, The parameter is the string name of the component class without the suffix "ViewComponent".
For example, if you have a view component class named `SampleViewComponent.cs`, then to invoke it put:
```html
<h1>Home</h1>
@await Component.InvokeAsync("Sample")
<p>This is a parent view</p>
```
###### Another Method To Invoke using tags
First is you import tag helpers and import the tag of the current project itself.
```cshtml
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper *, NameOfTheProject
```
Then you invoke it by 
```html
<vc:name-of-view-component></vc:name-of-view-component>
```
the name is converted to slug-case, because it is in the front. The Class name is of course in Pascal Case.
So for example you have a view component class named "EmployeeSalaryViewComponent.cs" then the tag should be:
```html
<vc:employee-salaries></vc:employee-salaries>
```
# What to learn or use it next?
- How to use View Data with View Components? [[View Components With View Data]].
- How to bind a model to a component view and create a strongly typed component view just like a [[Strongly Typed Views]] or [[Strongly Typed PartialView]]? answer: [[Strongly Typed View Components]].
- Because view component is made to be a more complex partial view with complex logic, that means you must be able to pass data from the view to the view component handler. see: [[ViewComponents with Parameters]].
- What if you want to load the component view dynamically? What if only after a press of a button you want to load the component view in the parent view? You return a [[ViewComponentResult]].