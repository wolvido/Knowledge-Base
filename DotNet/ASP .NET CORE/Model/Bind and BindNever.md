---
keywords: |-
  limit the properties accepted by a controller
  limit the type of data accepted by the controller
---
Specifies which properties of a view model should be included or excluded during model binding.
**`[BindNever]`** is an attribute used to indicate that a particular property of a model should never be included during model binding.
This is useful for security purposes, if you don't expect some data to come in it should not be included.

Sample:
```c#
public class UserModel
{
    public int Id { get; set; }
    
    [BindNever]
    public string Password { get; set; }
    
    [Display(Name = "User Name")]
    public string UserName { get; set; }
    
    [Display(Name = "Email Address")]
    public string Email { get; set; }
}
```

```c#
public class UserController : Controller
{
    // GET: /User/Register
    public ActionResult Register()
    {
        return View();
    }
    
    // POST: /User/Register
    [HttpPost]
    public IActionResult Register([Bind(nameof(user.UserName), nameof(user.Email))] UserModel user)
    {
	    //will only accept UserName and Email properties
        // Id will not be included and password will definitely not included
        // the excluded will be null
        return View("RegistrationConfirmation", user);
    }
}
```

