---
keywords: how does a controller find a view
---
- create a View folder
- Create a folder inside the View Folder with the same name as the Controller that renders it, and inside that folder, you put all the html views handled by that controller of the same name.
	For Example: You have a Controller named **HomeController**, and inside **HomeController** you have the action method **Index()**, so you create the folder structure: "/Views/Home/Index.cshtml".
>[!info]
>if you have an action method named **Index** inside a controller named **Home** then the default path of the html file corresponding the View Result will be in "/Views/**Home**/**Index**.cshtml", that is if you don't set a manual path.
> - The logic is: The path follows whatever the name of the Controller then the name of the action method.

## There is also the [[Shared Views]].