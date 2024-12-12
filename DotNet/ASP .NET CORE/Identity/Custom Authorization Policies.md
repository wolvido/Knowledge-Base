In rare instances, you might need an even more complex authentication than [[Role Authentication]], like for example you want to make a controller inaccessible if the user is logged in.
# How-To:

In this sample we will create a custom policy that will make the sign-up and sign-in aka the Account Controller inaccessible when the user is logged in. 

Assuming you've already set up the [[Authorization Policy]]. Inside `AddAuthorization(options =>{...})` add a custom policy.
```c#
services.AddAuthorization(options =>
{
	//create a custom policy
	options.AddPolicy("LoggedInOnlyPolicy", policy => //"LoggedInOnlyPolicy" is just a sample name for the policy
	{
		//this will decide the logic of the authorization
		policy.RequireAssertion(context =>  
		{ 
			//if this returns true, the controller or action is authorized, if false, then not authorized.
			
			//A condition that will return true if the user is not logged in.
			return ! context.User.Identity.IsAuthenticated;
		})
	});
});
```
###### Implement in the Controller or Action method.
```c#
public class AccountController : Controller 
{
	[Authorize("LoggedInOnlyPolicy")] //implement with Authorize attribute
	public Task<IActionresult> Register(RegisterDTO registerDTO)
	{
		//...
	}
	//Register page can only be accessed if user is logged-out
	
	[Authorize("LoggedInOnlyPolicy")]
	public async Task<IActionResult> Login(LoginDTO loginDTO)
	{
		//...
	}
	//Log-in page can only be accessed if user is logged-out
}
//Of course you can also implement the `[Authorize("LoggedInOnlyPolicy")]` on the whole controller itself.
```
If login/register page is accessed while logged in, it will redirect to Access Denied page, you can create the route to an Access Denied action method and page, or you can just create the route in an already existing action method.

>[!warning]
> be careful when implementing custom policies with `[AllowAnonymous]`, because allow anonymous will override everything. see [[Authorization Policy]] at the bottom to know about `[AllowAnonymous]`.