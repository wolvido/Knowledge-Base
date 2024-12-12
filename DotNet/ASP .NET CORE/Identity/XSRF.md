Cross-Site Request Forgery - CSRF is a process of making a request to a web server from another domain, using an existing authentication of the same web server. Eg. attacker.com creates a form that sends malicious request to original.com.
#### How does it work?
1. **Authentication**: The victim (user) is authenticated to a web application, often through cookies or session tokens.
   ![[Pasted image 20240501010036.png]]
   
1. **Malicious Website**: The attacker creates a malicious website which is mistakenly visited by the victim.![[Pasted image 20240501010101.png]]

2. **Automatic Execution**: When the victim visits the malicious website, their browser automatically sends a forged request to `bank.com/transfer` to transfer money using the victim's authenticated session.![[Pasted image 20240501010222.png]]

3. **Unauthorized Action**: Bank.com, seeing the request as coming from an authenticated user, processes it as a legitimate request and performs the action, such as transferring funds, changing account settings, or posting content.![[Pasted image 20240501010249.png]]
# Implement CSRF Tokens
In order to secure against XSRF we will implement anti forgery tokens. 
First is to use tag helpers in your forms([[Form Submission and link Tag helpers]]), then all you have to do is add the attribute `[ValidateAntiForgeryToken]` on the form action method. 
sample:
```html
<form asp-controller="Account" asp-action="Register" method="post">
	...
</form>
```
```c#
[HttpPost]
[ValidateAntiForgeryToken]
public Task<IActionresult> Register(RegisterDTO registerDTO)
{
	//...
}
```
`[ValidateAntiForgeryToken]` only works on Post requests, so usually it is applied with `[HttpPost]`.
But adding `[ValidateAntiForgeryToken]` on every `[HttpPost]` is tedious and it breaks DRY principle, so you add it as a filter.
###### You add the auto anti forgery filter in `.AddControllersWithViews(options => {...})`:
```c#
services.AddControllersWithViews(options => {
	options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute()); //add this
});
```
This will automatically add `[ValidateAntiForgeryToken]` on every POST request, so no need to add `[ValidateAntiForgeryToken]` on every `[HttpPost]`.
#### How it works?
![[Pasted image 20240501040921.png]]
The server splits the Anti-Forgery token into two: the cookie token and the form token, the server stores the cookie token in the cookies, and the form token as a hidden input in the form tag.
This way if the attacker has a prepared form, it will fail since it does not contain the form token.
Of course this is not foolproof, there are many way to acquire the form token still.

