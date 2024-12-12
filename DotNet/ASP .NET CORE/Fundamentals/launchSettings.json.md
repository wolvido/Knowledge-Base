It is a collection of key value pairs that configure various settings related to how the application should be launched and debugged. This file is typically found in the `Properties` folder of your web application project.

This configuration file is used **only in the development environment**.  You don't need launchSettings.json for publishing an app (on production server).
```json
{
	"profiles": {
		"IIS Express": {
			  "commandName": "IISExpress",
			  "launchBrowser": true,
			  "environmentVariables": {
				"ASPNETCORE_ENVIRONMENT": "Development"
			  }
		},
		"MyWebApp": {
			  "commandName": "Project",
			  "dotnetRunMessages": true,
			  "launchBrowser": true,
			  "applicationUrl": "http://localhost:5000",
			  "environmentVariables": {
				  "ASPNETCORE_ENVIRONMENT": "Development"
			  }
		}
	}
}
```
#### Profiles
Profiles is simply the setting profile on how the app will be launched by visual studio. In the sample above you have two profiles, you can choose which setting profile to use when launching the app.

In this Image below you can see three profiles we can switch to:
![[Screenshot 2023-12-20 231716.png]]
#### Key Value Settings

- The **"commandName"** maps to how the project should be started. Visual Studio uses this to run your project.
	- `IISExpress` obviously indicates that IIS Express is used to start the project.
	- `Project` indicates that the project is executed with the .NET CLI directly on the command line.
- **"dotnetRunMessages"** gives feedback messaged on dotnet CLI
- The **"launchBrowser"** property specifies whether the browser should be automatically launched when you start debugging the application.
- **"applicationUrl"** self explanatory
- **"environmentVariables"** the variables for the environment see: [[Environment]]. 
	- in **"ASPNETCORE_ENVIRONMENT"** you can set it for Development, Staging, or Production.

You can add, remove, or modify profiles in the `profiles` section to customize how your application is launched and debugged in different environments. This file allows you to control various settings related to debugging, such as the server, port, and environment variables.