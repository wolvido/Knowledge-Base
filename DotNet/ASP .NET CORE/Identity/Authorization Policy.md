Is a service that handles the authorization of a page. Prevents anyone from accessing a certain page without logging in or signing-up.
# How-To:
First, in `Program.cs` add:
```c#
app.UseRouting();
app.UseAuthentication();//reads the identity cookie
app.UseAuthorization(); //validates access to anything
app.MapControllers();//executes the whole pipeline
```
==**Make sure `UseAuthorization()` is above `MapControllers()` and below `UseAuthentication()`**==.
**Why the arrangement?** 
- Because the whole pipeline cannot be validated if the validation service runs after the pipeline.
- And also because the whole pipeline wouldn't know the authentication details if `UseAuthentication()` is initiated after `MapControllers()`.
- And also, it is suggested by Microsoft that it should all be below `UseRouting()`.
#### Register the service:
First, you add the service below the `services.AddIdentity...`, this is because it will need to use Identity. see: [[Registering Identity in IoC]].
```c#
services.AddIdentity<SampleUser, SampleRole>(
	...
)
//identity repository codes here...

//then add the authorization
services.AddAuthorization(options => {
	options.FallbackPolicy = new AuthorizationPolicyBuilder()
		.RequireAuthenticatedUser()
		.Build();
	//this builds an authorization policy aka users must be logged in to access all the action methods.
});

services.ConfigureApplicationCookie(options => {
	//if the user is not logged in, it will redirect here:
	options.LoginPath = "/Account/Login"; //"/Account/Login" is just a sample path, change as necessary.
	//this page is also exempt from authorization policy.
});
```
#### Allow Anonymous Authorization
In the sample above, it was set to prevent all action methods from being accesses without logging in, but what if you want to exempt certain sites from requiring authorization?
Simply add the attribute `[AllowAnonymous]` to a controller or an action method:
```c#
[AllowAnonymous]
public class HomeController: Controller
{
	...
}
```
Anyone can access all the action method of `HomeController` with or without logging in first. 
Don't forget you can also apply `[AllowAnonymous]` to an action method.
# What next?
[[Return URL]] - If the user fails to access a link because of not being signed-in, after signing-in it will automatically redirect to the failed link.