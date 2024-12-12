---
keywords: clean arch
---
Clean architecture is the invert of N-architechture. Instead of "business logic" depend on "data access logic", this dependency is inverted; it's "data access logic" depend on "business logic".
This makes the business logic cleanly separated, independent of data storage, UI, and is highly testable.
Also called "Onion Architecture" and "Domain-driven Design".

The business layer will be the Core of everything, everything will call the business layer even the Infrastructure layer(DbContext, repositories, and the external API calls). The goal is to keep the core business or application logic use cases independent of frontend and external frameworks. 
![[Pasted image 20240322172759.png]]
The infrastructure and the UI layer will call dependency on the core layer, the core will be completely independent.

When building an application using clean architecture, you start by defining the Entities and the business rules that the application must follow. From there, you build the application around those entities and the rules that expose them, keeping the different parts of the application separate and independent from each other. ==Essentially, the Entities is the core of everything, you build around them.== This makes the application more modular and easier to maintain and extend around the main purpose.

Clean architecture is suitable for all kinds of applications, but it is especially well-suited for applications that are expected to grow and change over time. This is because clean architecture is designed to promote modularity and flexibility, which makes it easier to make changes to the code without breaking existing functionality.

For extremely smaller applications that won’t require upscaling in future, we can use the traditional three-layer architecture (data access layer, business logic layer and presentation layer).
#### UI Layer and Initial File Structure
We start with the UI Project, we create the UI project first because the UI will contain the `Program.cs`. 
Create a new ''ASP Net Core Web App'' from the templates.
- The naming convention is to suffix the name with ".UI", sample: "ProjectName.UI".
- The Solution name should be "ProjectNameSolution" suffixed with "Solution".
- In the Solution (not the project folder), create two folders "src" and "tests". ''src'' will contain the layers and ''tests'' the test classes.
- Then move the entire UI project into src (just drag and drop).
We will add all the other layers in the src folder.
>[!question] Why is the `Program.cs` in the UI layer?
>Because the UI layer, also called the web layer, is responsible for configuring the web server and bootstrapping the ASP.NET Core application. The Core is still the core, and it must not concern itself with configuration, it must only focus on business logic.
#### The Layers
- [[Core Layer]]
- [[Infrastructure Layer]]
- [[UI Layer]]
- [[Tests - Clean Architecture]]