The UI layer is of course the UI. Also called the web layer; everything that functions the Frontend.
![[Pasted image 20240326184040.png]]
# How-To:
Assuming you already set up the UI layer as instructed in the parent note [[Clean Architecture]].
The UI layer will contain the following:
- "Controllers" folder, [[Controllers]].
- "Views" folder, [[View]].
- "Filters" folder, [[Filters]].
- "Middleware" folder, [[Middleware]].
- "StartupExtensions" folder, [[Arrange Program.cs]].
- "wwwroot" folder.
- "DTO" folder, if you need DTO to transfer from View to Controller only.
- And also the `appsettings.json` and `Program.cs.`
==If you are migrating from N-architecture, simply copy paste all of the mentioned above to the UI project.==
#### Dependencies
- In [[Clean Architecture]] everything depends on the core, so add a reference of the [[Core Layer]] to the UI project.
	- Right click on the dependencies of the UI project and add the core.
- you also need to add the [[Infrastructure Layer]] as dependency of UI layer.
- If you are using EF core in the [[Infrastructure Layer]] then you also might need to nuget install all the EF Core dependencies that you installed in [[Infrastructure Layer]].
- Nuget install the logging frameworks if there are any.

>[!question] 
>###### I don't get it, If [[Core Layer]] has repository interfaces/contracts folder to make it independent from [[Infrastructure Layer]], how come the [[UI Layer]] does not contain the service contracts?
> - Because that is not the point of clean architecture, if we put the service contracts in the UI layer, that means the core layer follows the UI layer. In Clean Architecture everyone follows the Core, the repository interfaces is located in the core so that the Core can work independently of the data source, In the case of the [[UI Layer]], the core itself is the data source, so it doesn't need the service contracts.
>  - In order to make UI and Core more encapsulated of each other, the DTO's in core layer is aimed only at the UI layer. There is no Core DTO aimed at infra, the repository contracts have that handled since the 