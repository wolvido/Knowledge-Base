The Core Layer is the core of Clean architecture.
![[Pasted image 20240322173128.png]]
# How-To:
>Assuming you are already familiar with N-Tier architecture(it's the architecture we've been using in the previous samples where everything is dependent in the data).

>Also assuming you already made the initial file structure and the UI layer, if not see the parent note [[Clean Architecture]]. 
#### Core
- In the src folder, right click and add a new class library.
- The naming convention is to add ".Core" as suffix, "ProjectName.Core".
###### File Structure
The Core project will contain the Business Logic and the Domain Layer. If not you're not migrating from another architecture, then just make the folders in the Core project.
- Create the "**Domain**" folder inside Core class library.
- Create the "**Entities**" folder inside "**Domain**" folder.
	- If migrating from N-Architecture, copy paste all the models in the old Entities folder, leave everything else, only the models.
- In the "**Domain**"  folder, also create the "**RepositoryContracts**" folder.
	- If migrating from N-Architecture, copy paste all the interfaces in the old RepositoryContracts folder, leave everything else, only the interfaces.
- Create the "**Exception**" folder inside Core class library.
	- If migrating from N-Architecture, copy paste all the exception classes in the old Exceptions folder, only the exceptions.
- Create the "**ServiceContracts**" folder inside Core class library.
	- If migrating from N-Architecture, copy paste all the interfaces in the old ServiceContracts folder, leave everything else, only the interfaces.
- Create the "**Services**" folder inside Core class library.
	- If migrating from N-Architecture, copy paste all the service classes in the old Services folder, leave everything else, only the service classes. Then in your services classes, remove all the unused namespaces that might cause errors, namespaces like EFCore.
- Create the "**Helpers**" folder inside Core class library. 
	- If migrating N-Architecture, inside the services folder, there is the old Helpers folder, copy paste all the helper classes to the new Helpers. see: [[DTO validation]].
	- Any reusable class that is not necessarily business logic is called Helpers. All reusable classes will be stored in helpers.
- Create the "**DTO**" folder inside Core class library.
	- If migrating from N-Architecture, copy paste all the DTO classes in the old DTO folder, leave everything else, only the DTO.
- If your project requires enumerations, create the **"Enums"** folder inside Core. Store all your Enumerations there.
- Also if you are migrating from another architecture, don't forget to install all the nuget packages from the old into Core project. In Visual studio, if you double click on the project name it will open the `csproj`; you will see all the installed packages.
- Related Notes: [[Entities]], [[custom exceptions]], [[Repository]], [[Services - Service layer]], [[DTO]], [[DTO validation]].
##### **Question**:
What's the difference between [[DTO]] and [[Entities]]?
- Entities are the core models of the project, its what we build the project around, DTO is so that we don't expose the Entities outside core layer, see: [[DTO]].
###### ==Why DTO's in the Core?==
- DTO's are the model's we use for the data that need to be exposed outside Core, while making sure entities are not exposed. So essentially to protect the Entities and separate concerns.  see: [[What's the point of DTO's]].
###### ==But why is there DTO separation between UI and Core, but not core and infra?==
- But there is a separation structure between Core and infra, its called the repository contracts, it enforced [[Dependency Inversion Principle (DIP)]] by making core independent of infra. DTO decouples data types, and core and infra should not have decoupled data types since the domain is and should be the purest type of data, infra's job is simply to provide that data. The only thing that should be decoupled and separated from infra and core is the implementation of the data access, that's why "**RepositoryContracts**" is in core.
- With UI to core, obviously we cannot create service contracts in the UI layer, since we don't need to inverse the dependency there, unlike Infra to core, the UI already depends on core, we just need to decouple the data, that's why there we encapsulate the core using DTO.
- So you see, essentially, Infra depends on core by implementing the repo contracts in core which makes core independent. The UI doesn't need to implement contracts from core, since UI already depends on core, they just need to decouple the data types.