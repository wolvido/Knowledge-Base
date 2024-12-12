---
keywords: |-
  how to handle exceptions for production
  how to handle exceptions for users
---
###### First, understand what this note is for, this note is for handling [[Exception]]s not for handling expected Invalid actions.
- If the user does invalid actions, then it should be handled gracefully, for example using: [[Tag Helpers]].
- If some exception does occur, then the user is not suppose to know everything it, it needs to be handled by try catch gracefully, depending on what you need it to get fixed and or inform the user,.
- SO essentially, there should be two types of error youre thinking about: 
	- and the one from users, which are the validations. Lookup this vault for how to work that.
	- and the unexpected errors called [[Exception]].
- If you're still confused about exceptions, see [[Exception]]. It explains there.

You have all the tools necessary to handle errors:
- [[How to throw an error]]
- [[Exception Handling Middleware]]
- [[Exception Filter]]
- [[custom exceptions]]
- [[UseExceptionHandler()]]
- [[Handling Form Validation Errors]] - for errors in forms to display.
#### But how do I handle exceptions in production environment? The one users see.
Well, it depends really, you already have the tools to handle it, you just have to read the context and decide on what's necessary.
- see some examples here: https://stackoverflow.com/a/48388586/13107848.
- See this: [Handle errors in ASP.NET Core | Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/error-handling?view=aspnetcore-8.0)
- You should use [[UseExceptionHandler()]] for the user error page.
Make sure that you separate the error handling for the development environment like this:
```c#
//if environment is development
if (app.Environment.IsDevelopment())
{
	app.useDevelopmentExceptionPage();
}

//or for staging
if (app.Environment.IsDevelopment() || app.Environment.IsStaging())
{
	app.useDevelopmentExceptionPage();
}

//or for custom
if (app.Environment.IsEnvironment("Beta"))
{
	app.useDevelopmentExceptionPage();
}
```
