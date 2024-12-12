There are two main Identity models:
![[Pasted image 20240328180744.png]]
- **IdentityUser`<T>`** is the user itself, `<T>` is the Id data type, recommended to use GUID for `<T>`. Of course you can inherit from this and create a child class that adds more properties such as address or TIN or etc., as many as necessary for your program.
-  **IdentityRole`<T>`** is the roles of the Users, you can create an "admin" or "employee" etc.. Of course you can also inherit from this and create a child class with additional properties.
# How-To:
- First, nuget install `Asp.NetCore.Identity`. 
	- ==If you are using NET 8, it's already built in, no need for a nuget package just import it:== `using Microsoft.AspNetCore.Identity;`
- Nuget install `Asp.NetCore.Identity.EntityFrameworkCore`. ==Only if you are using EFCore==.
	- If you are using [[Clean Architecture]] also install this on the UI layer, and Infra layer, not just the core.
#### Folder Structure:
Alongside Entities folder, create a new "IdentityEntities" folder, all the classes that inherit from `IdentityUser` and `IdentityRole` will be stored here.
#### Sample `IdentityUser` child:
```c#
public class ApplicationUser : IdentityUser<Guid>
{
	//all the properties from IdentityUser is here by default
	
	//Additional properties
	public string? PersonName {get; set;}
}
```
#### Sample `IdentityRole` child:
```c#
public class ApplicationRole : IdentityRole<Guid>
{
	//Add additional properties as necessary
}
```
#### Identity DbContext
Of course we will need a database to store our Identity objects.
The DbContext of Identities work differently, so instead of inheriting from `DbContext` we inherit from `IdentityDbContext`:
```c#
public class ApplicationDbContext : IdentityDbContext<ApplicationUser, ApplicationRole, Guid>
{
	public IdentityDbContext(DbContextOptions<IdentityDbContext> options) : base(options)
	{
	}
	
	//no need to add ApplicationUser and ApplicationRole Db sets, unless you want to add custom data for your Identities and Roles.
}
```
You do not need to create Db Sets for the identity models, `IdentityDbContext` automatically creates them just by adding them as generic parameters of `IdentityDbContext`. The first parameter of the `IdentityDbContext` generic is the name of the `IdentityUser` child, the second is `IdentityRole` child, the third is the data type used by `IdentityUser` and `IdentityRole` for their Id.
>[!warning] Important
>Don't get confused when making a DbContext, you can just replace inheritance from `DbContext` to `IdentityDbContext` and it will still work normally with non Identity Db Sets, **you dont need to create two separate DbContext**, DbContext is built-in.
>Of course you still can create separate DbContext if you want to.
###### If you decide to created a separate Identity DbContext, the you should separately register two `DbContexts`.
```c#
builder.Services.AddDbContext<AppDbContext>(options =>
{
    options.UseSqlServer(builder.Configuration.GetConnectionString("ConnectionString"));
});
builder.Services.AddDbContext<IdentityDbContext>(options =>
{
    options.UseSqlServer(builder.Configuration.GetConnectionString("ConnectionStringIdentity"));
});
```
- The sample above is registering both the a default `DbContext`, and the `IdentityDbcontext`, but you don't need to register an Identity Db context if you combined your `DbContext` on the default one.
###### You should also migrate it separately using `--context`.
Powershell Commands:
```powershell
dotnet ef migrations add IdentityMigration --context IdentityDbContext
dotnet ef migrations add AppMigration --context ApplicationDbContext

dotnet ef database update --context IdentityDbContext
dotnet ef database update --context ApplicationDbContext
```
DotNet EFCore commands:
```powershell
Add-Migration InitialIdentityMigration -Context IdentityDbContext

Update-Database -Context IdentityDbContext
```
this is assuming [[Code-First Migrations]].
>[!warning] # WARNING
> - Separated Db contexts means that EF navigation attributes will not be tracked by EF core and will cause dangerous errors. 
> - If you do insist on making separate DbContexts, you will have to **not** use the convention based on model navigation style taught here [[EF Table Relations]].
>  - If you need relations, then you just need to add a foreign key to the entity that requires a foreign key from a parent. Then if needed, have the services handle the data connections and relations.