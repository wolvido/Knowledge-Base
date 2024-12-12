The infrastructure layer grabs all the data that the program needs to run, essentially the infrastructure of the program. It composes of the repository, DbContext and the third party API calls.
![[Pasted image 20240325211501.png]]
# How-To:
- in the src folder, right click and add a new class library
- The naming convention is to suffix it with ".Infrastructure". Sample: "ProjectInfraName.Infrastructure"
#### Infrastructure Dependencies
- Install DB frameworks depending on what youre using, for example: `Microsoft.EntityFrameworkCore`.
- In [[Clean Architecture]] everything depends on the core, so add a reference of the [[Core Layer]] to the infrastructure project.
	- Right click on the dependencies of the infrastructure project and add the core.
#### DbContext
If using DB frameworks like EFCore, you will need to create a DB context. see: [[DbContext and DbSet]].
Inside the Infra project, create the folder "DbContexts", and store your DB contexts there.
	If migrating from N-Tier architecture, then copy paste DB context from the entities folder.
#### Code-First Migration
do if you plan on doing code-first migration, it works the same here [[Code-First Migrations]].
	If migrating from N-tier, do not copy the migration folder, create a new one in the Infrastructure project. [[Code-First Migrations]].
#### Repositories
Create a "Repositories" folder, and store your repositories there, assuming you know how a [[Repository]] works.
	If migrating from N-Tier, copy paste all repository classes into the Repositories folder.
