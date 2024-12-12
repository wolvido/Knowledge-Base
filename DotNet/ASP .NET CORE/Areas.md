Separate areas of UI functionality. 
![[Pasted image 20240426142816.png]]
**Why separate it?**
- The app is made of multiple high-level functional components that can be logically separated.
- You want to partition the app so that each functional area can be worked on independently.
- You want to create a meaningful [[Role Authentication]], so you create a separate Admin UI that can only be accessible by the Admin role. 
# How-To:
#### Create the Area
- If using [[Clean Architecture]] On your UI project right click and **New Scaffolded Item**, if not using clean architecture, then right click on your main project.
- On the templates, select MVC Area.
- On this sample we will create an Area for Admin, so lets name the area as "Admin".
###### It will create a Folder called "Areas" and inside will create a folder called "Admin". 
- A readme will also be created suggesting a conventional routing, ignore it if you're using attribute routing.
- The Admin folder will contain Controllers, Data, Models, and Views folders. You can delete the data folder if you have a data layer/Infrastructure layer set up on a separate project, the data folder here is an old architecture template, modern architectures have separate data layers/Infrastructure layers.
- Assuming we already have Controllers, Models, and Views that are separate from Admin, those are for general users. The one's in Admin will need to be built from scratch. The shared [[_ViewStart.cshtml]], [[Layout Views]], and [[_ViewImports.cshtml]] are not shareable to the area, **unless** you create a [[_ViewStart.cshtml]] in the root of the project(alongside `Program.cs`).
###### For example we'll create a controller for the Admin
Right click on controller folder in admin, and add controller. Let's name it "HomeController", just an initial name, change it as necessary:
```c#
[Area("Admin")]
public class HomeController : Controller
{
	[Route("[action]")]
	public IActionResult Index()
	{
		return View();
	}
}
```
==In order to specify that the controller is part of the Admin area and not the root, we need to add `[Area("Admin")]` attribute.==
#### Link Generation
To generate link to the areas from the root we need to use tag-helper `asp-area`
```html
<a asp-area="Admin" asp-controller="Home" asp-action="Index"> Admin/Home/Index </a>
```
This way, it does not navigate to index of the root, but the index of the Admin area.
###### But what if you are in the area, and you want to generate link from area to the root.
You leave `asp-area` as empty:
```html
<a asp-area="" asp-controller="Home" asp-action="Index"> /Home/Index </a>
```
This will navigate to the root index.