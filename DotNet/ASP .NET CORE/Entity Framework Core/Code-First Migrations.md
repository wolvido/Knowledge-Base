---
keywords: |-
  how to make a database
  make a database manually
---
>[!important]
>- In [[Clean Architecture]] or at least in Harsha's clean architecture, the UI layer needs to install all DB framework dependencies installed in Infrastructure.
>- And it needs to reference Infrastructure layer.
##### Migrations are changes in the model applied to the database. Will also include seed data if it exist.
![[Capture 43.png]]
# How-to:
#### Installation
- First, on your Entities class library, install `EntityFrameworkCore.Tools`.
- Then, on your **main project**, install `EntityFrameworkCore.Design`.
If using [[Clean Architecture]], install on the [[Infrastructure Layer]] and [[UI Layer]].
#### Add-Migration Command
**`Add-Migration`** is the command that will generate a migration file. A migration file represents a set of changes that need to be applied to the database schema to keep it in sync with the data model.
When you run this command, EF Core will examine your DbContext and compare it with the existing database schema to generate a migration file, essentially scaffolding a new migration. This means that Entity Framework Core examines the differences between your data model (defined in your code with classes and annotations) and the current state of the database. It then generates code (in the form of a migration file) to apply those differences to the database.
>[!warning]
> ###### **Make sure you set up your [[DbContext and DbSet]] first, before starting a migration.**
###### Open the nuget package manager console.
- open tools tab, then Nuget Package Manager, then Package manager console.
- Then on your Package Manager Console, make sure the Default Project: is set to the Entities class library, not the main project. If you don't see a Default Project, widen the console window.
	- If using [[Clean Architecture]], make sure the Default Project: is set to the Infrastructure layer.
	- Basically just set it to where the `DbContext`  is located.
###### Run the command: `Add-Migration MigrationName`
`MigrationName` is the name of the migration file. This will generate the migration file.
>[!note]
>Make sure to name the migration file appropriately depending on what you are migrating.
>for example if you are adding a new property to a model, and by extension adding a new column, then name the migration as `PropertyNameColumn`. If its the first migration, name it `Initial`. If youre updating a property `Property_Updated`. Name it properly as you see fit.
#### Migration API
The `Add-Migration` command will generate the "Migration" folder in the Entities class library, inside the folder will be two files.
The first file is your migration. It contains two methods, up and down.
- Up is executed while making changes to the tables or creating tables.
- Down is executed if you rollback the migrations.
These will be the method used when you implement your migration or roll it back.
#### Update-Database -Verbose
After creating the migrations, implement the migrations:
Go back to the console and Run the command: **`Update-Database -Verbose`**.
Verbose means to show all the sql script.
To undo a migration and delete the latest migration file, run `Remove-Migration`.
###### How to make changes after the DB has been created?
[[Change Table structure]]
###### How to create a Database manually without migrating?
- click on view tab and click on sql server object explorer.
- open the sql server and right-click on the database folder, and add new database.
- To get the connection string: right click on the created database, click properties, and copy connection string.
---
#### Mutiple DbContext
If you have multiple DbContext, you might need to specify which DbContext you want to migrate or update.
###### Powershell Commands:
```powershell
dotnet ef migrations add IdentityMigration --context IdentityDbContext
dotnet ef migrations add AppMigration --context ApplicationDbContext

dotnet ef database update --context IdentityDbContext
dotnet ef database update --context ApplicationDbContext
```
###### DotNet EFCore commands:
```powershell
Add-Migration InitialIdentityMigration -Context IdentityDbContext

Update-Database -Context IdentityDbContext
```
>[!warning] # WARNING
> - Separated Db contexts means that EF navigation attributes will not be tracked by EF core and will cause dangerous errors. 
> - If you do insist on making separate DbContexts, you will have to **not** use the convention based on model navigation style taught here [[EF Table Relations]].
>  - If you need relations, then you just need to add a foreign key to the entity that requires a foreign key from a parent. Then if needed, have the services handle the data connections and relations.
#### .NET Framework
[[code-first for .Net Framework]]