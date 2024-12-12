---
keywords: |-
  how to get data from backend to view
  how to get data from model to view
  Data from controller to view
  controller to view
---
Directly pass Model to the View. 
>[!info]-
> - Strongly-typed views are tightly bound to a model.
> - The strongly-typed view can receive model object (of specific model class) from the controller.
> - The controller can supply an object of the model by using the return View(model) method, at the end of action method.
### How it Works:
The Model:
```c#
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```
The Controller action method:
```c#
//sample string parameter: ?Id=2&Name=winz&Email=best email
public IActionResult Index(User? someUser)
{
    return View(someUser); //the object is passed on the return
}
```
The View:
```c#
@using NameOfProject.Models //import source of the view model
@model User //then assign User Class as the model of the view

<h1>Home</h1>
<h2>user: @Model.Name</h2>
<h2>user ID: @Model.Id</h2>
<h2>user Email: @Model.Email</h2>
```
>[!warning] DO NOT IMPORT VIEW MODELS DIRECTLY
>Do not add this: `@using View.Models //import source of the view model`. Instead it is advisable to use [[_ViewImports.cshtml]], the above is just for sample.

So if the sample query is **`?Id=2&Name=winz&Email=best email`** the output will be:
![[Capture 29.png]]
### What if I need multiple model to a single view?
**[[Strongly Typed Views multiple models]]**