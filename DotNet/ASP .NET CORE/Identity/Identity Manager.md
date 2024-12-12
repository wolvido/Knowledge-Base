It's the [[Services - Service layer]] of the Identity system. It contains all the methods/business logic for the [[Identity Models]].
###### There are two built in services for the Identity system: **`UserManager`**  and **`SignInManager`**.
![[Pasted image 20240415161920.png]]
# How-To:
- This is assuming you've already set up everything in the IoC ([[Registering Identity in IoC]]).
- Also that you've ==set up the database==. 
	- If not yet, then you need to migrate Identity DbCotext, see:[[Identity Models]].
	- After migrating, follow it up with `Update-Database` command.
- Also that you've already setup the View(Login, or signup, etc.) and its controller connection:
- And you've already created the child classes of [[Identity Models]] ==and its equivalent View only DTO==. if not see [[Validations for register form view model]].
>[!warning] Important
>Do not confuse the ==Core/service layer DTO== over ==View only DTO==, check bottom part of [[DTO]] if you forgot.
___
#### Sign-up using `UserManager`
Sign up manager provides business logic for managing users, its a service for managing users. Provides methods for CRUDing users. 
###### In this sample, we will use `UserManager` to register a `User`:
So this is assuming we have a `RegisterDTO` and a `SampleIdentityUser`.
In your controller, inject **UserManager** with the **IdentityUser** child:
```c#
public class AccountController : Controller //AccoutController is just a sample, change it as necessary
{
	private readonly UserManager<SampleIdentityUser> _userManager;
		//SampleIdentityUser is the IdentityUser's child, its just a sample change it as necessary.
		//if your confused about SampleIdentityUser see: IdentityModels note.
	
	public AccountController (UserManager<SampleIdentityUser> userManager)
	{
		_userManager = userManager;
	}
	
	//Then in your action method, bind the view model/DTO
	[HttpPost] //needs to be post or else it will send an empty form for every reload
	public Task<IActionresult> Register(RegisterDTO registerDTO)
	{
		//THIS IS VERY IMPORTANT: use tag helper client validation for the validation
		
		//map the DTO to the SampleIdentityUser Identity
			SampleIdentityUser user = new SampleIdentityUser() {
				UserName = registerDTO.UserName,
				Email = registerDTO.Email};
			//notice we did not set the password here.
			
		//create the user using UserManager
		//store the password here so it becomes a hash
		IdentityResult result = await __userManager.CreateAsync(user, registerDTO.Password); 
			//IdentityResult is the built in return for Identity operations- 
			//it contains the status result after executing the operation,-
			//in case of success or failure it contains the appropriate message.
			
		if (result.Suceeded)
		{
			//here we add the persist sign in
			//if sign-up is successfull, client will receive persist sign-in token, so they keep logged-in.
			await _signInManager.SignInAsync(user, isPersistent: true);
				//you can also set this to false and have a "keep me logged in" checkbox to set it to true.
				//this will create a persistent identity cookie in the client.
				
			//if no error then proceed
			return RedirectToAction(//redirect to dashboard or index etc...);
		}
		else
		{
			//if some mistake, then add the errors in model state
			foreach (Identity error in result.Errors)
			{
				ModelState.AddModelError("RegisterError", error.Description);
				//This way the error will be sent to the asp-validation-summary and be displayed to the user.
				//thats why I said its IMPORTANT earlier.
				//"RegisterError" is just a key, change it as necessary, the value is the error description.
				
				//go back to the register view because it failed
				return View(registerDTO);
			}
		}
	}
}
```
>[!warning]
>This is very much untested, see questions in https://www.udemy.com/course/asp-net-core-true-ultimate-guide-real-project/learn/lecture/34524908#questions if error ever occurrs
---
#### `SignInManager`
Sign-in manager provides business logic for signing-in users, its a service for signing-in users. Provides methods for sign-in functionality of users and handles authentication cookie for keeping users signed-in.
##### Login system using `SignInManager`:
- Assuming you already have a `LoginDTO` and you've already set up the view and all its tag helpers and validation tag helpers.
```c#
public class AccountController : Controller 
{
	private readonly UserManager<SampleIdentityUser> _userManager;
	private readonly SignInManager<SampleIdentityUser> _signInManager;
	
	public AccountController (UserManager<SampleIdentityUser> userManager, SignInManager<SampleIdentityUser> signInManager)
	{
		_userManager = userManager;
		_signInManager = signInManager; //inject sign in manager
	}
	
	[HttpGet] //get version when navigating the login page, you dont want to post an empty login form
	public IActionResult Login()
	{
		return View();
	}
	
	[HttpPost] //post only works when submitting data, it doesnt accidentally activate in navigation
	public async Task<IActionResult> Login(LoginDTO loginDTO)
	{
		//login using _signInManager, it checks if account exists
		var result = await _signInManager.PasswordSignInAsync(loginDTO.Email, loginDTO.Password, isPersistent: false, lockoutOnFailure: true);
			//persistent false will log out the user when he leaves the browser
			//alternatively, you can create a "keep me logged in" checkbox to set it to true
			//lockoutOnFailure will lock the user for too many failed attempts
		
		if (result.Succeeded)
		{
			return RedirectToAction(//redirect to dashboard or index etc...);
		}
		else
		{
			//if failed, then add the identity validation errors to asp-validation-summary
			ModelState.AddModelError("LoginError", "Invalid email or password");
				//this error is hard coded cause its just short, but you can follow the method above if needed.
				
			return View();
		}
		
	}
}
```
#### Logout
logout is very simple:
```c#
public async Task<IActionResult> Logout()
{
	await _signInManager.SignOutAsync();
	return RedirectToAction(//Index or outside);
}
```