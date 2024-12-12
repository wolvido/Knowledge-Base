To perform a code-first migration in .NET Framework with Entity Framework 6, follow these steps:

### 1. Set Up Your DbContext
[[DbContext and DbSet]] it might be slightly different for .net framework.
### 2. Install Entity Framework Package
Make sure Entity Framework 6 is installed via NuGet. Run this command in the **Package Manager Console**:
```bash
`Install-Package EntityFramework`
```
### 3. Enable Migrations
Run this command in the **Package Manager Console** to enable migrations:
```bash
`Enable-Migrations`
```
This command creates a `Migrations` folder in your project with a `Configuration.cs` file.
### 4. Create a New Migration
To create a new migration script, use the following command in the **Package Manager Console**:
```
`Add-Migration InitialMigration`
```
Replace `InitialCreate` with a descriptive name for your migration. This will generate a new migration file under the `Migrations` folder.
### 5. Apply the Migration
To apply the migration and update the database, run this command:
```bash
`Update-Database`
```
This command will execute the `Up()` method in your migration class and create the database schema as defined in your `DbContext`.

**Note that you don't need to create a database, it will be created automatically, but if you want you can also create manually.**
### Additional Tips
- **Customizing the Configuration**: You can edit `Configuration.cs` to set properties like `AutomaticMigrationsEnabled` or specify which database initializer to use.
- **Updating the Database**: After adding new changes to your models, you need to run `Add-Migration` again and then `Update-Database` to apply changes.
- **Reverting Changes**: If you need to revert a migration, use `Update-Database -TargetMigration: PreviousMigrationName`.

This setup should help you get started with code-first migrations in .NET Framework 4.8 using Entity Framework 6.