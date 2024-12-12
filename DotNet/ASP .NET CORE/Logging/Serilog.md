---
keywords: File Sink
---
One of the most popular logging framework for asp.net. has many features that are not supported by asp built-in logging.
The main advantage is that serilog can store the log in external destinations such as the database, or files, the built in cant do that.
>[!info] Reminder
>Don't get confused, Built-in ILogger is still used with serilog once serilog is registered.
###### Sinks
in Serilog the destination of the log is called a sink. Serilog supports many sinks, the most common are:
- Console
- Debug
- EventLog
- File
- Database
- Seq
- Azure
# How To:
- First is to nuget install **Serilog** in your main project.
- then nuget install another one called **Serilog.AspNetCore**.
Then in program.cs register serilog:
```c#
builder.Host.UseSerilog(
	(HostBuilderContext context, IServiceProvider services, LoggerConfiguration loggerConfiguration) =>
		{
		    loggerConfiguration
		        .ReadFrom.Configuration(context.Configuration)
			        //Read the configuration settings in appsettings and apply.
		        .ReadFrom.Services(services);
			        //Read all the current services and make them available to serilog.
		}
);
```
UseSerilog accepts a lambda with 3 arguments:
- **Context** to register the HttpContext. (see: [[What is HttpContext or context]]).
- **Services** (as in the [[IoC]] of the application), to register the services.
- **Configuration** of the logger, which will represent its configuration of course.
###### Now in your appsettings, add the serilog configuration:
```json
"Serilog": {
	"Using": [ 
		"Serilog.Sinks.Console",
		"Serilog.Sinks.File"
		//set here where to sink, in this sample we set it in console and file
	], 
	"MinimumLevel": "Debug", //the minimum level of logging layer, here it is set to debug.
	
	//WriteTo is where we write additional configuration for teh sinks
	"WriteTo": [ 
		  {
			  "Name": "Console" 
			  //just the name for the console since it has no additional config
			  //if you register a sink, you have to write its name in WhereTo even if there's no config.
		  },
		   {
			"Name": "File",
			"Args": { //configure the path for the file and etc..
				"path": "Logs\\log.txt", //assuming you have a logs folder in you project, if not create it.
				"rollingInterval": "Day", //every day a file is created
					//can be hour, day, month, year, etc..
				"retainedFileCountLimit": 7, //maximum number of log file retained
				"fileSizeLimitbytes": 1048576, //1mb
				"rollOnFileSizeLimit": true
					//will create a log once fileSizeLimitbytes is reached, even if interval is not reached
			}
	      }
	],
	//enrichers will be explained below
	"Enrich":[
		"FromLogContext"
	],
	"Properties":
	{
		"ApplicationName": "Super Good App",
		"ApplicationVersion": "1.00"
	}
  }
```
The sample above uses Console Sink and **File Sink**.
#### Enrichers
Enrichers are additional details that are added to **LogContext**. For example the name of the machine or some custom property.
![[Pasted image 20240227180529.png]]
###### What is the **`LogContext`**?
It is used to dynamically add and remove properties from the ambient "execution context".
For example, all log messages written during a transaction might carry the id of that transaction, or name of the machine or some custom property. **Essentially, it allows you to add context to every log.**
```json
"Enrich":[
	"FromLogContext"
],
"Properties":
{
	"ApplicationName": "Super Good App",
	"ApplicationVersion": "1.00"
}
```
This configuration means that every log message will include a key value pair showing the "ApplicationName" and the "ApplicationVersion".
![[Capture 47.png]]
 "ApplicationName" and "ApplicationVersion" will show up along with the other log properties.
# What Next:
- Above is for File Sink, Learn Serilog for Database Sink [[Serilog Database Sink]].
- What if you need to view the logs in real time as the user is using? and in a structured way, see: [[Serilog Seq]].
- Enrichment properties are static, and it is the same or all log messages of every request. What if you need a custom dynamic property that will log the service methods and other backend? see [[IDiagnosticContext]].
- What if you need to log the amount of time it took to execute code? see: [[Serilog Timings]].
- Logging best practice [[Structured Logging - Serilog]].