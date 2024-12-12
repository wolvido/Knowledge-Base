Also known as **sproc**. Perform complex database operations with a single call.  
A prepared SQL command so that you can save in the database, so the code can be reused over and over again.
I'm not sure exactly where and when to use this over LINQ, maybe depends on the architecture and the situation.
# How-To
>[!Warning]
>- When registering the sproc, this note is using code-first approach. Might not be applicable for DB-first approach.
>- But when retrieving/using the sproc, it is the same doesn't matter what approach.
>
>Also, we will be using ApplicationDbContext from the previous samples. see: [[DbContext and DbSet]].
#### Migration Up
Since we are using code-first approach, we will register the sproc in the Up method of the migration file. This is assuming you know what a migration file is, if not see: [[Code-First Migrations]].
In your Migrations file:
```c#
public partial class GetPersons_StoredProcedure : Migration
{
	protected override void Up(MigrationBuilder migrationBuilder)
	{
		//sp_GetAllPersons is the sproc to be registered in the DB itself.
		//dbo is the default schema.
		//sprocs exist in the database not the code, it is only called by the code.
		string sp_GetAllPersons = @"
			CREATE PROCEDURE [dbo].[GetAllPersons]
			AS BEGIN
				SELECT PersonId, PersonName, Email, Gender FROM [dbo].[Persons]
			END
		";
		//The name of the sproc in this sample is GetAllPersons.
		
		//register the sproc in the SB
		migrationBuilder.Sql(sp_GetAllPersons); 
	}
	
	//If there is an Up theres a Down, for if you want to remove the sproc.
	protected override void Down(MigrationBuilder migrationBuilder)
	{
		//to remove the sproc, simply DROP and the name of the sproc.
		string sp_GetAllPersons = @"
			DROP PROCEDURE [dbo].[GetAllPersons]
		";
		migrationBuilder.Sql(sp_GetAllPersons);
	}
}
```
Then you can run **`Update-Database`**. see: [[Code-First Migrations]] if you don't know what that means or how to do it.
##### Naming Convention: 
- when naming a migration for a sproc use `ProcMethodName_StoredProcedure` - sample: `GetPersons_StoredProcedure`.
- When naming the sproc itself, use `sp_SprocName` - sample: `sp_GetAllPersons`. Also use this when naming the method that calls the sproc.
###### DBO syntax for creating a Read/Get sproc:
![[Pasted image 20240130173034.png]]
>[!info]
>This is for a read/get sproc. Syntax is different for a sproc that inserts, updates, deletes because those require parameters to insert. The sproc for CUD with parameters is shown below.
#### Calling the Sproc
On your `DbContext` class, below your `OnModelCreating`, create a method that calls your sproc:
```c#
public List<Person> sp_GetAllPersons()
{
	//again the name of the sproc in this sample is GetAllPersons
	return Persons.FromSqlRaw("EXECUTE [dbo].[GetAllPersons]").ToList();
	//the return collection is converted To List since the original return type is not practical to use.
}
```
###### Then on your service
simply call it in your service method. Sample:
```c#
public List<Person> GetAllPersons()
{
	return _personsDb.sp_GetAllPersons();
}
```
If you're confused, it works exactly like LINQ, but instead the code is in the database and you just call it. 
# Stored Procedure for Input and Delete
The sample above shows a sproc that reads/gets data. 
For a sproc to input data and delete data, we need to have parameters for the sproc, like a function.
When registering, it works the same way as the sample above. You write the sproc syntax in the Up method of the migration.
Here is a sample of sproc to insert data:
```c#
public partial class InsertPerson_StoredProcedure : Migration
{
	protected override void Up(MigrationBuilder migrationBuilder)
	{
		//warning: the code might not make sense if you dont expand obsidian notes to a good width
		string sp_InsertPerson = @"
			CREATE PROCEDURE [dbo].[InsertPerson]
			(@PersonId uniqueidentifier, @PersonName nvarchar(40), @Email nvarchar(40), @Gendernvarchar(10))
			AS BEGIN
				INSERT INTO [dbo].[Persons](PersonId, PersonNamem Email, Gender) VALUES (@PersonID, @PersonName,
				@Email,@Gender)
			END
		";
		migrationBuilder.Sql(sp_InsertPerson);
	}
	
	protected override void Down(MigrationBuilder migrationBuilder)
	{
		string sp_InsertPerson = @"
			DROP PROCEDURE [dbo].[InsertPerson]
		";
		migrationBuilder.Sql(sp_InsertPerson);
	}
}
```
###### Syntax explanation:
```sql
--Declaration--
CREATE PROCEDURE [dbo].[InsertPerson] 
--Parameters--
(@PersonId uniqueidentifier, @PersonName nvarchar(40), @Email nvarchar(40), @Gendernvarchar(10))
--Insert--
AS BEGIN
	INSERT INTO [dbo].[Persons](PersonId, PersonNamem Email, Gender) VALUES (@PersonID, @PersonName,
	@Email,@Gender)
END
```
###### 1. Declaration
```sql
CREATE PROCEDURE [dbo].[InsertPerson]
```
Declares a stored procedure named `InsertPerson` within the `dbo` schema.
###### 2. Parameters
```sql
(@PersonId uniqueidentifier, @PersonName nvarchar(40), @Email nvarchar(40), @Gender nvarchar(10))
```
This line declares four input parameters, the input parameters are based on the registered table columns in the database. 
This is the columns you will insert to in the DB, so the parameters uses the exact DB column type of each.
If you dont know what to put here, look up the column type equivalent in the sql server object explorer. It's usually in the `Database/DdName/Tables/dbo.TableName/Columns`.
###### 3. Insert
```sql
AS BEGIN
	INSERT INTO [dbo].[Persons](PersonId, PersonName, Email, Gender) VALUES (@PersonID, @PersonName, @Email, @Gender)
END
```
This line is an SQL `INSERT` statement. It inserts a new row into the `Persons` table in the `dbo` schema. The values for the columns are provided from the input parameters of the stored procedure.
- `PersonId`, `PersonName`, `Email`, and `Gender` are the column names in the `Persons` table.
- `@PersonID`, `@PersonName`, `@Email`, and `@Gender` are the values passed as parameters to the stored procedure.
#### Calling the Sproc
On your `DbContext` class, below your `OnModelCreating`, create a method that calls your sproc:
```c#
public int sp_InsertPerson(Person person)
//return type is int because the sql command we will execute returns the number of rows affected
{
	//here we convert each value of Person into an sql parameter to feed into the Sproc
	SqlParameters[] parameters = new SqlParameters[]
	{
		new SqlParameters("@PersonId", person.PersonId),
		new SqlParameters("@PersonName", person.PersonName),
		new SqlParameters("@Email", person.Email),
		new SqlParameters("@Gender", person.Gender)
	};
	
	//here we execute the command that will feed the parameters to the sproc we made
	return Database.ExecuteSqlRaw("EXECUTE [dbo].[InsertPerson] @PersonId, @PersonName, @Email, @Gender", parameters);
}
```
###### Then on your service
simply call it in your service method. Sample:
```c#
public void AddPerson(Person person)
{
	_db.sp_InsertPerson(person);
}
```
>[!warning]
>This is just for sample, you rarely use void methods for crud of a service. You should consider passing [[DTO]]'s even for insert methods.
###### DBO syntax for creating a CUD sproc:
![[Pasted image 20240130203835.png]]
# What next?
from the info you learned above, you can extrapolate how to Update and delete.


