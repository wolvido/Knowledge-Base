These views can be accessed by any controller. Normally the controller can only access the views contained in the folder with the same name as that controller and under the view folder.

Shared Views are placed in "Shared" folder under "Views" folder:
Views
	Shared
		SharedView.cshtml
### So for example:
you have a home controller:
```c#
public class HomeController : Controller
{
    public IActionResult Index()
    {
        return View();
        //So naturrally, it will render the file in /Views/Home/Index.cshtml
        //but if Index.cshtml does not exist in Home then it will search in Shared folder
    }
}
```
Every Controller will search in "Shared" folder.
![[Capture 32.png]]