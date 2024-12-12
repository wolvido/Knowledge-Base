You already know there are [[User Roles]]. We can authenticate pages, pages where only the customer role or the admin role should be able to access. We authenticate access using [[Role Authentication]], the pages are separated using [[Areas]].![[Screenshot 2024-04-26 at 19-00-00 Asp.Net Core 8 (.NET 8) True Ultimate Guide 1.png]]
# How-To:
- Assuming you already set up [[User Roles]] and the [[Areas]], [[Identity Models]], DTO's, and [[Identity Manager]].
###### In this sample we will use an "Admin" Area, and we will make it only accessible by the Admin Role.
#### Log in with Role
Assuming we've already set up the Login view and connected it to the controller, and assuming we've already set up the `_userManager` in the controller. If not see [[Identity Manager]].
When logging in, we need to check if the user login is an admin, if it is an admin, redirect to Admin Area.
```c#
[HttpPost]
public async Task<IActionResult> Login(LoginDTO loginDTO)
{
	if (!ModelState.IsValid )
	{
		ViewBag.Errors = ModelState.Values.SelectMany(temp => temp.Errors).Select(temp => temp.ErrorMessage);
		return View(loginDTO);
	}
	
	var result = await _signInManager.PasswordSignInAsync(loginDTO.Email, loginDTO.Password, isPersistent: false, lockoutOnFailure: false);
	
	if (result.Succeeded )
	{
		//grab the user by the provided email when logging in
		SampleIdentityUser user = await _userManager.FindByEmailAsync(loginDTO.Email);
		if (user != null) //if user exist
		{
			//check if his role is admin, use IsInRoleAsync
			if (await _userManager.IsInRoleAsync(user, UserTypeOptions.Admin.ToString() ) )
			{
				//if it is admin, redirect to admin area
				return RedirectToAction("Index", "Home", new { area = "Admin" });
					//This is assuming the controller name is Home, change it as necessary.
					//and also assuming the Area is named admin.
			}
		}
		
		return RedirectToAction(nameof(PersonsController.Index), "Persons");
	}
	else
	{
		ModelState.AddModelError("Login", "Inalid email or password");
	}
	
	return View(loginDTO);
}
```
**`return RedirectToAction("Index", "Home", new { area = "Admin" });`** This code will redirect to index of the Admin [[Areas]]. 
#### `.IsInrole()`
In case you need to show an element only if the user is the correct role, you will use `.IsInrole()`, sample:
```html
@if (User.IsInRole("Admin"))
{
	<a asp-controller="Home" asp-action="Index" asp-area="Admin"> Admin home</a>
}
```
will only show the element if the user is in Admin role.
#### Role Based Authentication
Role based authentication is implemented using a predefined filter provided by Identity.
Assuming you know [[Areas]]. Let's say we already an Admin Area.
In your Admin Area controller, add the attribute `[Authorize(Roles = "role1,role2,role3...")]`:
```c#
[Area("Admin")]
[Authorize(Roles="Admin")] //You can write more than one role, comma separated
public class HomeController : Controller
{
	//can also be applied to action method of course not just the whole controller
	//[Authorize(Roles="Admin")]
	public IActionResult Index()
	{
		return View();
	}
}
```
`[Authorize(Roles="Admin")]` means that only admin role users can access this controller, preferably separated by an [[Areas]].
#### Don't Confuse Harsha's dumbass tutorials
You don't need to create [[Areas]] just to limit certain parts to certain roles. 
You just need: `[Authorize(Roles="Admin")]` to limit a controller or an action method to Admin only.
# What next:
- [[Custom Authorization Policies]] - In rare instances, you might need an even more complex authentication than [[Role Authentication]], like for example you want to make a controller inaccessible if the user is logged in.