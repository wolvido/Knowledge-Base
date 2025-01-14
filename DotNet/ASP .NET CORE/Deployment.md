[[Environment]]

I'm not sure where to start... But the main concept is, when doing code first migration:
1. have a database online ready, 
2. then grab the connection string of that database, 
3. then add the connection string on appsetting alongside the default, 
4. and in your program.cs set that connection string only if running production. 
```c#
//sample
if (!builder.Environment.IsDevelopment()) //If not in development environment
{
    builder.Services.AddDbContext<AccountDbContext>(options =>
    {
        options.UseSqlServer(builder.Configuration.GetConnectionString("ConnectionStringFromDBServer"));
    });
}
```
5. Then open the repo in powershell, navigate to the repo,
6. set the environment to production, see: ([[Process Level Environment]]).
7. then run `dotnet ef database update` command. The the DB will be set.
8. After the DB is set, Publish the code on visual studio or something.

#### Command line code for code first migration
[Applying Migrations - EF Core | Microsoft Learn](https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/applying?tabs=dotnet-core-cli#command-line-tools)
first set your environment to non dev that points to the production database
___
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