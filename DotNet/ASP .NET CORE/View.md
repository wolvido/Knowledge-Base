What is view? The frontend basically. More specifically the frontend is the View Presentation Logic. 
The controller connects the [[Model]] to the corresponding view presentation logic.
### How do we add a view?
**First**, before anything else, we must add the s­­tupid p­­re­requis­ites in progra­m.cs­­­
```c#
builder.Services.AddControllersWithViews();
var app = builder.Build(); //you already have this, just add the two samples above and below this line of code
app.UseStaticFiles();
```
### Folder Structure
- create a View folder
- Create a folder inside the View Folder with the same name as the Controllers that render it, and inside that folder, you put all the html views handled by that controller of the same name.
	For Example: You have a Controller named **HomeController**, and inside **HomeController** you have the action method **Index()**, so you create the folder structure: "/Views/Home/Index.cshtml".
>[!info]
>if you have an action method named **Index** inside a controller named **Home** then the default path of the html file corresponding the View Result will be in "/Views/**Home**/**Index**.cshtml". (That is if you don't set a manual path).
> - The logic is: The path follows whatever the name of the Controller then the name of the action method.
### How To Render a view
to render a view, you return a View Result, it is handled by the controller
```c#
[Route("/home")]
public IActionResult Index()
{
	return View(); //View() returns a View Result to the client, see IActionResult for more info
		//This View Result will render /Views/Home/Index.cshtml.
}
```
The rendering needs a frontend cshtml file to render. Naturally it will throw an error without a frontend file.

If you wish to set a manual path for the view result:
```c#
[Route("/home")]
public IActionResult Index()
{
	return View("sample"); //will search for sample.cshtml in /Views/Home/sample.cshtml
	//if we use the default
	
	//return View(); //will register to /Views/Home/Index.cshtml
}
```
The parameters of `View()` method is used to point it to the file path and send model data. Without parameters it will render the the view on the default path and pass no data. See [[View() Helper Method]] for more info.
### The View Presentation Logic
- Rendering a View without a View file itself would run error, create the cshtml first.
>[!info]-
>This is assuming you already know how to make frontend html, js, css, etc.. if not see [[FrontEnd]].
- So assuming you have the cshtml ready, simply connect it using the default pathing or set a manual pathing.
- The Frontend will be handled by the Frontend code, and for the server side scripting we use [[Razor Views]]. 
>[!question] where do I put frontend static files like images or the css, js?
>[[Web Root and UseStaticFiles()]]
#### Navigation
you navigate from one view to an action method by using links of course.
The links will then point to an action method route, which the action method will generate the destination view.
```html
<p>You can reach Winzy at:</p>
<ul>
  <li><a href="About/Website">Website</a></li>
</ul>
```
If the link is pressed then it will lead to action method:
```c#
[Route("About/Website")]
public IActionResult WinzylWebsite()
{
    return View(); //by default will render WinzylWebsite.cshtml
}
```
>[!warning]
>We don't usually use manual route paths, it is better to use tag helpers to point to the right action method see: [[Form Submission and link Tag helpers]].
### What do I need to know after this?
- Go to [[Razor Views]] to know server side scripting in a view.
- Then see [[Strongly Typed Views]] to know how to pass data from model object to the view.
- Then [[Shared Views]] to know how to do shared views that can be accessed by anything.
- Then [[_ViewImports.cshtml]] to know how to use shared imports, so you don't have to import models on all views.
- Next [[Layout Views]] to create view templates like site header, footer, the things that are persistent in a site, you know like a header that carries about, contacts, etc.., also used to not repeat js or css linking. 
- What if you need a specific layout for that one view only, or you need dynamically changing layouts depending on user actions? You use [[Dynamic Layouts]].
- What if I don't want whole layout to dynamically change, what if I only need a section of a layout to change or add a specific css or js to this view only. You use [[Section Layout Views]].
- Then [[_ViewStart.cshtml]] to manage the Layout views. 
- next is [[Partial Views]], can be used as a reusable BEM block to be invoked anywhere or if you need anything to be reusable, like a razor function on many views. Very useful for DRY. You can use it to add a shareable reusable elements to a view.
- Now when you need a Partial View with complex business logic, you should use [[View Components]]. Basically just like Partial views but has its own self contained business logic.
- How do I send data from view to controller? [[form-urlencoded and form-data]].
- For client side validation, use this [[Client Side Validations tag helpers]].