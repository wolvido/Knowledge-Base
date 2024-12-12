# How-To:
#### Install Rotativa and wkhtmltopdf.exe
First you have to understand how it works. It works by converting a View into a PDF. This means you need to separate or create a clean view without layouts and stuff. It uses Rotativa and wkhtmltopdf.exe.
- Nuget Install `Rotativa.AspNetCore` in your main project.
- download wkhtmltopdf zip version, open the "wkhtmltopdf" file, open bin, copy the "wkhtmltopdf.exe".
- in your wwwroot create a "Rotative" folder, paste the "wkhtmltopdf.exe" inside.

Then in your program.cs register "wkhtmltopdf.exe" to Rotativa by adding:
```c#
Rotativa.AspNetCore.RotativaConfiguration.Setup("wwwroot", wkhtmltopdfRelativePath: "Rotativa");
//This is assuming you stored it in wwroot/Rotativa folder, if not edit as neccessary
```
#### View
As mentioned before, it converts a view into pdf. So you might need a clean view without layouts, links, etc.. 
You can use a pure partial view or create a separate view that is for pdf generation only. 
Creating a new view for pdf generation only **might** be a bad design, but not prohibited.
#### Action method
In your Action method, you need to use `ViewAsPdf()`.
sample:
```c#
public IActionResult PersonsPdf()
{
	//Get view model data from a service
	List<Person> persons = _personService.GetAllPersons();

    return new ViewAsPdf("nameOfView", persons, ViewData)
    {
	    //optional properties, will be set to default if empty.
		PageMargins = { Left = 20, Bottom = 20, Right = 20, Top = 20 },
		PageSize = Rotativa.AspNetCore.Options.Size.A4,
		PageOrientation = Rotativa.AspNetCore.Options.Orientation.Portrait
    };
}
```
This will automatically generate a pdf from the view.
>[!question] why is **ViewData** a parameter of ViewAsPdf()?
>  of course almost every controller has a ViewData, and more likely you have data on your ViewBag/ViewData that is needed in your pdf view. So, it almost always gets passed as a parameter in **`ViewAsPdf()`**.
Syntax:
```c#
ViewAsPdf("nameOfView", model, ViewData)
{
	//properties... 
}
```
>[!Warning]
>Since you are dealing with a database and a website, it might be necessary to **async** the methods, see: [[EF Core Async]] or [[Asynchronous Async]]. The samples above are non-async. Simply convert it to async.
The samples above and below are not async. You will also async the action methods.

>[!info]
>I don't need to mention this, but just in case you forget. You execute this by adding a route attribute to the action method and a link or a button on a view that leads to the action method, that link/button will be the download button and will automatically download the file to the client.
