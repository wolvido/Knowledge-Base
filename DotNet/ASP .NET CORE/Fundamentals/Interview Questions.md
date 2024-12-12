see: [[Basic Knowledge .NET CORE]] for the basics
**What is Asp.Net Core meta package?**
The ASP.NET Core shared framework (Microsoft.AspNetCore.App) contains assemblies that are developed and supported by Microsoft. Microsoft.AspNetCore.App is installed when the .NET Core 3.0 or later SDK is installed. The shared framework is the set of assemblies (.dll files) that are installed on the machine and includes a runtime component and a targeting pack. It is Included in the .csproj file.
```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>
    ...
</Project>
```

**When do you choose classic ASP.NET MVC over ASP.NET Core?**
On most cases use core, on legacy use MVC

**What is a web application framework, and what are its benefits?**
Tools and libraries that help developers to write, maintain and scale applications. They provide tools and libraries that simplify the above recurring tasks, eliminating a lot of unnecessary complexity.

**What is Kestrel?**
Kestrel is an event-driven, I/O-based, open-source, cross-platform, and asynchronous server which hosts .NET applications. It is provided as a default server for .NET Core.

**What is the difference between IIS and Kestrel? Why do we need two web servers?**
The main difference between IIS and Kestrel is that Kestrel is a cross-platform server. It runs on Windows, Linux, and Mac, whereas IIS only runs on Windows.
Kestrel doesn’t provide all the rich functionality of a full-fledged web server such as IIS, Nginx, or Apache. Hence, we typically use it as an application server, with one of the above servers acting as a reverse proxy.

**What is the purpose of launchSettings.json in asp.net core?**
The launchSettings.json file is used to store the configuration information, which describes how to start the ASP.NET Core application, in Visual Studio. see [[Knowledge Base/DotNet/ASP .NET CORE/Fundamentals/launchSettings.json]]

**What is a host in in .NET Core?**
a host in .NET provides a runtime environment for your application, offering services and infrastructure to manage the application's execution and configuration.

**What is generic host or HostBuilder in .NET Core?**
.NET generic host called ‘HostBuilder’ helps us to manage all the below tasks.
- Dependency Injection
- Service lifetime management
- Configuration
- Logging
The generic host was previously present as ‘Web Host’, in .NET Core for web applications. Later, the ‘Web Host’ was deprecated and a generic host was introduced to cater to the web, Windows, Linux, and console applications.

**What is the purpose of the .csproj file?**
The project file is one of the most important files in our application. It tells .NET how to build (compile) the project.
The csproj file stores list of package dependencies of the current project, target .net version and other compilation settings.
```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
<PropertyGroup>
  <TargetFramework>net6.0</TargetFramework>
</PropertyGroup>

<ItemGroup>
  <PackageReference Include="PackageName" Version="1.0.0.0" />
</ItemGroup>
</Project>
```

**What is the “Startup” class in ASP.NET core prior to Asp.Net Core 6?**
The startup class is the entry point of the ASP.NET Core application. Every Asp.NET Core (Asp.Net Core 5 and earlier) application must have this class. It contains the necessary code to bootstrap the application. This class contains two methods Configure() and ConfigureServices().
- Configure(): The Configure() method is used to essential middleware(s) to the application request pipeline.
- ConfigureServices(): The ConfigureServices() method is used to add services to the IoC container.

In Asp.Net Core 6 (.NET 6), Microsoft unifies Startup.cs and Program.cs into a single Program.cs.
In asp.net core 6 (and up), we need to add all such as registering middleware to the application pipeline, adding services to the IoC container, configuring the ‘application configuration’, configuring the logger, authentication and adding DbContext in Program.cs file.

**What does WebApplication.CreateBuilder() do?**
Loads the configuration, environment, and default services.