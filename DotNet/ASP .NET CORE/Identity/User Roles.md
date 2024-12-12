There are user roles like Customer Role, Admin Role, Employee Role etc.. Identity has built in service methods and database to register and manage the roles.
# How-To:
- This is assuming you've already set up [[Identity Models]], [[Validations for register form view model]], [[Identity Manager]], [[Authorization Policy]].
#### In this sample we will create two roles, the `Admin` and a general `User`.
###### first, create an enumeration for the two roles:
```c#
public enum UserTypeOptions
{
	User, Admin
}
```
>[!question] Where to create Enums folder?
>its like DTO. If you are using clean architecture, it depends on where it is used, if it's like a view model DTO, then store it in UI layer, if its used by the business logic, then store it in Core. 
___
###### In your view model/RegisterDTO, the one you use to transfer data from the register page to controller, add `UserTypeOptions`:
```c#
public class RegisterDTO
{
	//assume there are other properties here like Username and Password
	
	public UserTypeOptions UserType {get; set;} = UserTypeOptions.User;
		//default is User
}
```
==Don't forget to import the enum in the model.==
###### In your Register or Login view form, create a radio button or whatever you need for the selection of the role:
```html
<div>
	<input type="radio" id="User" asp-for="UserType" value="User" checked />
	<label for="User">User</label>
	
	<input type="radio" id="Admin" asp-for="UserType" value="Admin" />
	<label for="Admin">Admin</label>
</div
```
So, when registering or logging in, the user can choose the appropriate role.
#### Backend
In your Register action method, setup the Role:
```c#
public class AccountController : Controller 
{
	private readonly UserManager<SampleIdentityUser> _userManager;
	private readonly SignInManager<SampleIdentityUser> _signInManager;
	//create role manager
	private readonly RoleManager<SampleIdentityRole> _roleManager;
		//SampleIdentityRole is just a sample identity child class, change it as necessary, see Identity Models note.
	
	public AccountController (UserManager<SampleIdentityUser> userManager, SignInManager<SampleIdentityUser> signInManager, RoleManager<SampleIdentityRole> roleManager)
	{
		_userManager = userManager;
		_signInManager = signInManager;
		_roleManager = roleManager; //inject
	}
	
	[HttpPost]
	public Task<IActionresult> Register(RegisterDTO registerDTO)
	{
		SampleIdentityUser user = new SampleIdentityUser() { UserName = registerDTO.UserName, Email = registerDTO.Email};
		IdentityResult result = await __userManager.CreateAsync(user, registerDTO.Password); 
			
		if (result.Suceeded)
		{
			if (registerDTO.UserType == Core.Enums.UserTypeOptions.Admin) //assuming you stored the Enums folder in Core
			{
				//check if admin role exists
				if (await _roleManager.FindByNameAsync(UserTypeOptions.Admin.ToString() ) is null)
				{
					//if not then make one
					SampleIdentityRole sampleRole = new SampleIdentityRole() {
						Name = UserTypeOptions.Admin.ToString()
					};
					await _roleManager.CreateAsync(sampleRole); //create the role
				}
				
				//then add the new user into the newly created admin role
				_userManager.AddToRoleAsync(user, UserTypeOptions.Admin.ToString() );
					//this will automatically insert into the Identity database.
			}
			else
			{
				//else its the user role
				_userManager.AddToRoleAsync(user, UserTypeOptions.User.ToString() );
					//No need to create a User role, Identity already has that table built-in.
				
			}
			
			await _signInManager.SignInAsync(user, isPersistent: true);
			
			return RedirectToAction(//redirect to dashboard or index etc...);
		}
		else
		{
			//redirect to the same page and register the errors
		}
	}
}
```

In the database in table `AspNetRoles` you will see a new `Admin` role.
In `AspNetUserRoles` you will see the new user registered to the new role, all connected foreign keys using GUID. 