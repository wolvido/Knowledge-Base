---
keywords: |-
  automatically check for existing 
  Validation that checks the database
  magic validation
---
When a user inputs an already existing email or username, then the server will have to check the database for existing values and if it exists, it will have to refresh the page, but there is a way to validate existing values instead of having to check the database and refresh the page.
This allows the server and client to prevent unnecessary request and unnecessary wait time for the user.
>[!Important] Can be used on any Input, not just for [[identity]].
# How-to:
It's achieved by using creating an action method that performs the validation then import that action method to the model property by using the `[Remote]`.
>[!info]
> - This is assuming you already know what `UserManager` and `SignInManager`, if not see: [[Identity Manager]].
> - Assuming you've already connected a register form to the controller and action method.
> - assuming youve already connected validation through [[Client Side Validations tag helpers]].
###### ==First==, in the project where the View Model/DTO is located, NuGet install: `.Mvc.ViewFeatures`.
#### Action Method Validator
```c#
public class AccountController : Controller 
{
	private readonly UserManager<SampleIdentityUser> _userManager;
	private readonly SignInManager<SampleIdentityUser> _signInManager;
	//SampleIdentityUser is just sample child of the Identity Models, change it as necessary.
	
	public AccountController (UserManager<SampleIdentityUser> userManager, SignInManager<SampleIdentityUser> signInManager)
	{
		_userManager = userManager; // inject user in manager
		_signInManager = signInManager; //inject sign in manager
	}
	
	//checks if email is already registered
	public async Task<IActionResult> IsEmailRegistered(string email)
	{
		//we will use FindByEmailAsync method of UserManager to check for any email.
		SampleIdentityUser user = await _userManager.FindByEmailAsync(email);
		
		if (user == null) //check if user with the email exist
		{
			//the remote validation from the browser can only receive a json result.
			return Json(true); //user with email does not exist yet
		}
		else
		{
			return Json(false); //user with email already exist
		}
	}
{
```
#### `[Remote]` Attribute
After creating the action method validator implement the validation on your view model/DTO:
```c#
public class RegisterDTO
{
	[Remote(action: "IsEmailRegistered",  controller: "Account", ErrorMessage = "Email is already registered")]
	public string Email { get; set;}
}
```
[[Client Side Validations tag helpers]] will automatically implement. Of course this is not only used for Email, you can create for Username or phone number or whatever.
>[!important]
>Can only use action methods not services.