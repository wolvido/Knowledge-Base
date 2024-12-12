The environment of the program. What affects it and what it can affect.
#### Software Development Lifecycle Environment
- **Development Environment:** The space where developers write, test, and debug code.
- **Staging Environment:** A testing environment that closely mirrors the production environment for comprehensive testing before deployment.
- **Production Environment:** The live or operational environment where the final, fully-tested version of the application is accessible to end-users.
#### IWebHostEnvironment
You can check all about the environment by calling the various methods of IWebHostEnvironment in program.cs
```c#
//this is in program.cs
app.Environment.//there are many methods and properties, look at sample below or look at intellisense
```
Methods and Properties:
```c#
//to get or set the environment via program.cs
app.Environment.EnvironmentName = "Development";

//to get or set the absolute path of the app via program.cs
app.Environment.ContentRootPath = /C:/Absolute/Path;

//more below
```

To make sure to never show the exception page on the Production Environment. You can do this by adding this code in program.cs:
```c#
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
# What next?
- you can set the environment in [[launchSettings.json]].
- When you have to access the current working environment programmatically in the controller see: [[Environment in Controller]].
- It is rare, but in case you need an html tag that enables or disables depending on the environment, you use [[Environment tag helper]].
- [[launchSettings.json]] configurations are only used in development environment and by visual studio. So how do you set up environment configurations in staging or production environment? see: [[Process Level Environment]].