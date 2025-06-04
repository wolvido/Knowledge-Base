---
keywords: how to get database connection string
---
A DbContext class is binded to an SQL Database and vice versa:![[Capture 42.png]]
- DbContext is a general class that is the object representation of the DB, and each property is a type of DbSet that accepts the generic of a model. This class is responsible for tracking entity changes, managing transactions, and translating LINQ queries into SQL commands. Think of it as a bridge between your C# code and the database.
- A DbSet is the object representation of a single table. Just like DbContext but for the Entities/table.
# How-to:
#### File Location and Dependencies
- Create an "Entities" class library project. You can put the DbContext file there.
- Then on the "Entities" class library project, nuget install `Microsoft.EntityFrameworkCore.SqlServer.`
	- **disclaimer**: in this sample we will use Azure SQL database. `Microsoft.EntityFrameworkCore.SqlServer` uses Azure SQL database provider.
	- or you can use `Microsoft.EntityFrameworkCore.Sqlite` for SQLite.
	- or for the full list of databases providers see: [Database Providers - EF Core | Microsoft Learn](https://learn.microsoft.com/en-us/ef/core/providers/?tabs=dotnet-core-cli)
- ~~Then on the main project, you also have to install install `Microsoft.EntityFrameworkCore.SqlServer`, since different layer and all.~~
- If you are using [[Clean Architecture]], you put the DbContext in the [[Infrastructure Layer]], and also that's where you nuget install the dependencies.
#### Naming Convention
- postfix a DbContext file with "DbContext".
	sample: `public class ApplicationDbContext`
- a DbSet name must be plural, to signify that it is a set of the model.
	sample:`public DbSet<Country> Countries {get; set;}`
#### Model/Entities
Add a primary key to your models, by using `[key]` attribute.
sample:
```c#
public class Person
{
    [Key] //means main key
    public int PersonId { get; set; }
    public string? Name { get; set; }
}
```
Then make sure your properties are properly limited to a reasonable amount of character.
For example for name and email set it to 40 characters:
```c#
public class Person
{
    [Key] //means main key
    public int PersonId { get; set; }
    [StringLength(40)]
    public string? Name { get; set; }
    [StringLength(40)]
    public string? Email { get; set; }
    [StringLength(10)] //you can set gender to 10
    public string? Gender { get; set; }
}
```
set the length whatever is needed appropriately.
>[!info]
>- You don't need to add `[Key]` if the main key is named appropriatley, like `PersonId`, EF core already knows by the name.
>- For the complete list of model attributes that translate into DB see: [Code First Data Annotations - EF6 | Microsoft Learn](https://learn.microsoft.com/en-us/ef/ef6/modeling/code-first/data-annotations)
#### Create the DB Context and DbSets
On the Entities create a class, postfix it with "DbContext" and inherit from DbContext. (theres a different folder for clean arch see: [[Infrastructure Layer]]).
Then create DbSets of the models.
Sample:
```c#
public class ApplicationDbContext : DbContext
{
	//Default constructor to inherit from the base and inject the options later
	public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options)
	 {
	 }
	 
	public virtual DbSet<Person> Persons {get; set;}
	public virtual DbSet<ModelSample> ModelSamples {get; set;}
}
```
DBContext can have more than one DbSet.
>[!info]
>- DbSets need to be virtual so it can be overriden my mock testing later on. See [[Mocking]] for sample.
>- you can convert the constructor into primary constructor version.
#### Bind to table
After creating the DbSets, we need to bind them to the tables.
To do that we need to override `OnModelCreating` on the same DbContext class:
```c#
public class ApplicationDbContext : DbContext
{
	//Default constructor; to inherit from the base and inject the options later
	public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options)
	 {
	 }
	 
	public virtual DbSet<Person> Persons {get; set;}
	public virtual DbSet<ModelSample> ModelSamples {get; set;}
	
	protected override void OnModelCreating(ModelBuilder modelBuilder)
	{
		base.OnModelCreating(modelBuilder); //to construct the parent class
		
		//Here we bind DbSet Persons to the Persons Table
		modelBuilder.Entity<Person>().ToTable("Persons"); //Persons is the name of the table.
		//Essentially tells EF Core that you are going to configure the mapping for the "Person" entity.
		//once you have the Person entity `.ToTable("Persons");` then maps Person entity to a DB Table named Persons.
		
		modelBuilder.Entity<ModelSample>().ToTable("ModelSamples");
	}
}
```
>[!info] Another Info
>- You can configure everything in `ModelBuilder`, including tables, indexes, primary keys, or relations, or any seed data. Literally everything in the DB.
>- Don't get confused about the configuration commands, read about it here [[Fluent API]] or here [Fluent API - Configuring and Mapping Properties and Types - EF6 | Microsoft Learn](https://learn.microsoft.com/en-us/ef/ef6/modeling/code-first/fluent/types-and-properties)
#### DB Connection string
Before we can connect to the DB, we need its connection string.
**To get the connection string:**
- click on view tab and click on sql server object explorer.
- If you have no existing database or you want to make a new one, open a server instance, right click on databases folder and add a new one.
- open databases folder and right click on your database, click properties, and copy connection string.

Once you have the connection string, it needs to be stored of course, but it is essentially an api key, so it needs to be stored into config see:[[Configurations]], it shouldn't be hardcoded.

By Convention, the connection key must be stored on a parent `"ConnectionStrings"`. I highly recommend storing your connection string on on a parent  named `"ConnectionStrings"`.
```json
"ConnectionStrings": {
  "DefaultConnection": "Data Source= YourDbConnectionString..."
  //note: you can name "DefaultConnection" anything you want, but "ConnectionStrings" is a convention.
}
```
Once you have the connection string configured, You can just use the key instead of the whole thing.
In this sample, lets assume the key is `"ConnectionStrings:DefaultConnection".
#### DbContext as a Service
Once you have the Connection string, just like any other service, register the DbContext in program.cs.
But before you can do that, you first need to add Entities class library as a project reference to the main project and to import it in program.cs.
	- This will be [[Infrastructure Layer]] instead of Entities class library if using [[Clean Architecture]].
	- and main project will be [[UI Layer]].
In this sample we will use .UseSqlServer() since we are using an Sql Server. This can be set differently to different servers like sql lite or mysql or something, depending on what you're using.
To register it:
```c#
builder.Services.AddDbContext<ApplicationDbContext>(options => 
        options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"))
	        //we dont need to put "ConnectionStrings:ConnectionStrings" 
	        //"DefaultConnection" is enough, GetConnectionString() will automatically set inside
    );
```
>[!warning]  
>`GetConnectionString("DefaultConnection")` might not work if you did not store "DefaultConnection" in "ConnectionStrings" by convention. 
#### Usage
Now we can inject the DB to other services, assuming you know how to inject, if not see: [[Services - Service layer]].
Sample:
```c#
public class SampleService : ISampleService
{
	private readonly ApplicationDbContext _db
	
	public SampleService(ApplicationDbContext applicationDbContext)
	{
		_db = applicationDbContext;
	}
	
	//sample method
	public List<Person> GetPerson(string name)
	{
		return _db.Persons.Where(person => person.Name == name);
		//Persons is a DbSet, which means a collection of Person type.
		//db is a DbContext.
	}
	
	//all the other methods...
}
```
>[!warning] Important
>It might not be a good idea to directly **connect a Service to a database/Injecting a database to a Service**, It might be better to implement a [[Repository]]  also see: [[Inject Repository to Service]] if you already have one.
