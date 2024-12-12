is a partial view that is bound to a specified model class.
Basically a [[Strongly Typed Views]] but in partial views.
### How?
Simply import the model to the partial view, just like in [[Strongly Typed Views]]:
```html
//import the model into this partial view
@model SampleModel 

<section>
	//html code etc..
</section>
```
>[!tip] Reminder
>Also don't forget to add a **@using View.Models** in your [[_ViewImports.cshtml]].

Then, supply the model object to the invocation in the parent view:
Parent View:
```html
<partial name = "_SamplePartialView" model = "sampleModel"></partial>
```
This way, the partial view becomes **Extensible**. 
Because you see, you can supply different model objects to two different partial views in the same parent view.
sample:
```html
<partial name = "_SamplePartialView" model = "sampleModel"></partial>

<partial name = "_SamplePartialView" model = "sampleModel2"></partial>
```
This will invoke two different partial views with different data objects using, using and displaying different data's in on parent view.
#### Use View Model Aggregates
If you are using [[Strongly Typed PartialView]], and your main view has a Model, Use a DTO aggregate and pass the property, https://stackoverflow.com/a/15043516.
>[!warning]
>##### Only use this if you really have no choice. 
>This has problems with validation tag helpers, the best practice is for your parent view to have no Aggregate model or strongly typed model, and only partial views should have a model.
>##### Or you should use [[PartialViewResult]] instead.
>

For example:
```csharp
public class LoginViewModel
{
    [Required(ErrorMessage="Username is Required")]
    public string Username { get; set; }

    [Required(ErrorMessage = "Password is Required")]
    public string Password { get; set; }
}
```
And for the register partial:
```csharp
public class RegisterViewModel
{
     [Required(ErrorMessage="Username is Required")]
     public string Username { get; set; }

     [Required(ErrorMessage = "Password is Required")]
     public string Password { get; set; }
}
```
And then your main view model should aggregate those 2 view models:
```csharp
public class MyViewModel
{
    public LoginViewModel Login { get; set; }
    public LoginViewModel Register { get; set; }
}
```
Then in your main view:
```html
<partial name="~/path" model="Model.Login"></partial>
<partial name="~/path" model="Model.Register"></partial>
```
**This is to make sure that if your DTO has required properties, you wont have to initialize it unnecessarily, especially if the partial is a form.**
#### Other methods of Invoking Strongly Typed Partial View:
- `@await Html.Partial("_SamplePartialView", sampleModel)`
- `@{ await Html.RenderPartialAsync("_SamplePartialView", sampleModel); }`
