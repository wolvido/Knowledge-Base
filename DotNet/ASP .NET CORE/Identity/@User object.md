---
keywords: display username
---
`@User` is a razor variable containing the current User object, or the lack thereof.
You can use it to check if the user is logged in or to know the name of the current logged-in user.
#### Check If a user is logged in
If logged in display the log-out button, else display the log-in and sign-up button.
```html
<div>
@if (@User.Identity.IsAuthenticated) //if logged in
{
	<a asp-controller="Account" asp-action="Logout">Log-out</a>
}
else
{
	<a asp-controller="Account" asp-action="Login">Log-in</a>
	<a asp-controller="Account" asp-action="Signup">Sign-up</a>
}
</div>
```
#### How to have the current logged in user have a username displayed in a view
Like for example:
![[Capture 50.png]]
In the view add: **`@User.Identity?.Name`**, this gives the current logged in user. Sample:
```html
<div class="username">
	@User.Identity?.Name
</div>
```
Then in **`Program.cs`** add the authentication middleware:
```c#
app.UseRouting();
app.UseAuthentication(); //reads the identity cookie
app.MapControllers(); //executes the whole pipeline
```
###### Make sure `UseAuthentication()` is directly above `MapControllers()`.
And also it is suggested by Microsoft that it should be below `UseRouting()`.
Why? Because the whole pipeline wouldn't know the authentication details if it was initiated after `MapControllers()`.
