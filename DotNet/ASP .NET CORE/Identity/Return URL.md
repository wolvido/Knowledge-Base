If the user fails to access a link because of not being signed-in, after signing-in it will automatically redirect to the failed link.
![[Pasted image 20240422183947.png]]
![[Pasted image 20240422183956.png]]
![[Pasted image 20240422184021.png]]
![[Pasted image 20240422184123.png]]
# How-To:
So once you set up your login path in the cookie configuration:
```c#
services.ConfigureApplicationCookie(options => {
	//if the user is not logged in, it will redirect here:
	options.LoginPath = "/Account/Login";
});
```
It will automatically add a Query string `ReturnUrl`, that contains the link that the user failed to access due to not being signed in. 
**"/Account/Login"** is just a sample for the login page action method path. Change it as necessary.
>[!info] 
>- If you forget what `.ConfigureApplicationCookie(...)` is, see [[Authorization Policy]] first.
>- if you forget what query string is, see [[Model Binding Acceptable Data]] and [[FromQuery and FromRoute]].
##### So assuming the controller is **Account** and action method that handles the login is **Login.**
So in the login page form add `asp-route-ReturnUrl`:
```html
<form asp-controller="Account" asp-action="Login" asp-route-ReturnUrl="@Context.Request.Query['ReturnUrl']" method="post">
```
**`"@Context.Request.Query['ReturnUrl']"`** gets the value of `ReturnUrl`.
#### Return URL
**On Login Page**: When a user attempts to access a protected resource that requires authentication, they may be redirected to the login page with a `ReturnUrl` query parameter. Once authentication is accepted, a return URL needs to be available.
To implement:
```c#
[HttpPost] 
public async Task<IActionResult> Login(LoginDTO loginDTO, string? ReturnUrl) //add ReturnUrl as parameter
{
	var result = //assuming you already set this up, if not see Identity manager.
	
		if (result.Succeeded)
		{
			//check if there is a ReturnUrl and if the Url is not an external Url
			If (!string.IsNullOrEmpty(ReturnUrl) && Url.IsLocalUrl(ReturnUrl))
			{
				return LocalRedirect(ReturnUrl); //redirect to the ReturnUrl, the one that failed before loging-in.
				
				//checking if ReturnUrl is local only is extremely important-
				//as it prevents attackers from injecting a malicious site.
			}
			
			//if ReturnUrl is empty or a non-local, and login is correct, then simply redirect normally.
			return RedirectToAction(//redirect to dashboard or index etc...);
		}
		else
		{
			ModelState.AddModelError("LoginError", "Invalid email or password");
			return view();
		}
}
```
