---
keywords: |-
  multiple input on single property in view model 
  Submit more than one value in one view model property
  accept multiple model object
---
#### If you need to accept multiple data into one view model property you use:
```c#
public class Book
{
	public List<string?> Genre { get; set; } = new();
}
```
If book model has multiple Genre make it a list.
**and**
The data being received by the backend needs to be indexed in order to register in the list
![[Capture 26.png]]
You can arrange the indexing in the accepting frontend or if the frontend does not return an indexed Genre you can arrange it in a [[Custom Model Binder]].
#### If you need to accept multiple of a model into the controller:
One method is you can just make it a list in the controller itself:
```c#
public class HomeController : Controller
{
    public IActionResult Index(List <Book> Books)
    {
        return View(Books);
    }
}
```
on your imports you can put:
```html
@using Weather.Models //put this on _ViewImports
@model List<CityWeather>
```
see: [[_ViewImports.cshtml]]
**Sample:**
![[Capture 33.png]]