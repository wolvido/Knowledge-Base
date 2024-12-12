The syntactic sugar of ViewData. See [[ViewData]].
>[!Warning]
>Do not use ViewData or ViewBag to pass model data, use [[Strongly Typed Views]] to pass model data. 
>- ViewData or ViewBag is mostly used to pass meta data and other special cases see: [MVC ViewBag Best Practice](https://stackoverflow.com/questions/11262034/mvc-viewbag-best-practice). 
>- This sample passes model data just to demonstrate how to pass data using View Data, to be beginner friendly. 
>And also because the bad Harsha course uses "beginner friendly" bad samples.

**Instead of doing ViewData like this:**
```html
@using View.Models
@{
    User? someUser = (User?)ViewData["UserProfile"]; 
}

<p>Some user: @someUser?.Id</p>
<p>Some user: @someUser?.Name</p>
<p>Some user: @someUser?.Email</p>
```
**You can just do this:**
```html
<h1>Home</h1>
<h2>Some user: @ViewBag.user.Name</h2>
<h2>Some user: @ViewBag.user.Id</h2>
<h2>Some user: @ViewBag.user.Email</h2>
```
The controller:
```c#
public class HomeController : Controller
{
    public IActionResult Index(User user) //data is taken from request and model binded to be a user object
    {
        // ViewData["UserProfile"] = user; //The ViewData method
        ViewBag.user = user; //do this instead of the ViewData method
        return View();
    }
}
```
Without the importing anything, without typecasting anything.
See [[ViewData]] for the full context and sample.
>[!Warning] Again
>Do not use ViewData or ViewBag to pass model data, use [[Strongly Typed Views]] to pass model data. 
>- This sample passes model data just to demonstrate how to pass data using View Bag, to be beginner friendly. 
>And also because the bad Harsha course uses model data sample.

![[Capture 27.png]]