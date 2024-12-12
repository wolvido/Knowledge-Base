- ViewData is a dictionary-like object that passes the data from controllers to views.
- It is dictionary-like, meaning it is composed of key-value pairs, specifically it is derived from `IDictionary<KeyValuePair<string, object>>` it has key of string type and value of object type. Every key value is paired to an object.
- It is created when a controller action method renders a view result.
- You can directly access it using **`ViewData["key"]`**.
>[!Warning]
>Do not use ViewData or ViewBag to pass model data, use [[Strongly Typed Views]] to pass model data. 
>- ViewData or ViewBag is mostly used to pass meta data and other special cases see: [MVC ViewBag Best Practice](https://stackoverflow.com/questions/11262034/mvc-viewbag-best-practice). 
>- This sample passes model data just to demonstrate how to pass data using `ViewData`, to be beginner friendly. 
>And also because the stupid Harsha course uses "beginner friendly" shitty samples.

>[!Warning] Another Warning
>If you really need to use ViewData. Use [[ViewBag]] instead, it is the syntactic sugar version. But again, ViewData or ViewBag is rarely used, use [[Strongly Typed Views]].
### How to use it to pass data from view model object to view presentation logic
Model:
```c#
public class User
{
	public int Id { get; set; }
	public string Name { get; set; }
	public string Email { get; set; }
}
```
Controller:
```c#
public class HomeController : Controller
{
    public IActionResult Index(User user) //data is taken from request and model binded to be a user object
    {
        // Setting the user object in ViewData
        ViewData["UserProfile"] = user;
        return View();
    }
}
```
View:
```html
@using View.Models
@{
    User? someUser = (User?)ViewData["UserProfile"]; 
}

<p>Some user: @someUser?.Id</p>
<p>Some user: @someUser?.Name</p>
<p>Some user: @someUser?.Email</p>
```
**``user``** object in **``ViewData["UserProfile"]``** is casted back to **`User`** because the Value type of the **`ViewData`** Key-Value pair is of object type , specifically it is `IDictionary<KeyValuePair<string, object>>` it has key of string type and value of object type.
>[!Warning]
> Again, It is not advisable to use this method of passing view model objects, this is just for demonstration purposes to teach the fundamentals and be comprehensive.
