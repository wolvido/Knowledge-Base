The first filter. As the name suggest it handles authorization. It check if the user is authenticate or not before proceeding.
![[Pasted image 20240307150227.png]]
###### Authorization Filter only has one method **`OnAuthorize`**, because it only needs to authorize before the pipeline, there is no after authorization.
###### Purpose of **`OnAuthorize`**:
- Determines if the user is authorized for the request.
- Short-circuit the pipeline if the request is NOT authorized. [[Filter Short Circuit]].
- **`OnAuthorize`** should not throw exceptions, that is the job of [[Exception Filter]], Its job is to short circuit in case of invalid authorization. An Invalid Authorization in essence is **not an [[Exception]].**
# How-To:
**Assuming you know how to make filters and its folder and how to attribute it**, if not read again [[Filters]].
###### Non-async Syntax:
```c#
public class SampleAuthorizationFilter : IAuthorizationFilter
{
	public void OnAuthorization(AuthorizationFilterContext context)
	{
		//authorization logic
	}
}
```
for the Async version [[Asynchronous Filter]].
###### Sample:
We will verify whether the token is submitted in the cookie
```c#
public class TokenAuthorizationFilter : IAuthorizationFilter
{
	public void OnAuthorization (AuthorizationFilterContext context)
	{
		//we will read all the cookies submitted from the browser to server, and verify them
		//"Auth-key" is a key that is paired with a value that says the user has logged in before, 
		//so the user can be logged in automatically
		if (context.HttpContext.Request.Cookies.ContainsKey("Auth-key") == false) 
		{
			//"Auth-key" does not exist, then the client has not logged in before and-
			//cannot be logged in automatically
			
			//Short-circuit since it is not verified
			context.Result = new StatusCodeResult(StatusCode.Status401Unauthorized);
			//you can short-circuit it any way you want-
			//StatusCodeResult(StatusCode.Status401Unauthorized) is simply used in general
		}	
	} 
}
```
Actually not explained by harsha, so need to learn cookies first.