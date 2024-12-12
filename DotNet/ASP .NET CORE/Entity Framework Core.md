A n object relational mapping commonly used by .NET applications. Its what you use to access the database using OOP.
Cross-platform and lightweight.

It works by binding one table per model, and one column per property of the model. Like so:![[Capture 40.png]]
>[!info]
>For larger projects, might be better to use Dapper
#### EFCore Approaches
There are two approaches when developing with EFCore; DbFirst Approach and CodeFirst Approach.
![[Capture 41.png]]
- In DbFirst Approach, you create the Db values first then convert it to models.
- In CodeFirst, you convert the models into Db values.
###### Essentially:
- CodeFirst is usually used in initial development or in small projects.
- DbFirst is usually used in large projects, or if there already exists a DB.
>[!warning]
>By Default, an EF core injection is singleton scoped, you might encounter a captive dependency if the DB is injected to a non singleton service. see: [[Best Practice for Services and DI]], see: [[Transient, Scoped, Singleton]].
# How-To do EF Core:
1. [[DbContext and DbSet]] - learn this first before anything else.`
2. [[Seed Data EFCore]] - Initial set of data when the DB is created.  Useful for setting up a known data state for testing, development, or deploying an application for the first time.
3. [[Code-First Migrations]] - Migrations are changes in the model applied to the database.`
4. [[Change Table structure]] - edit table once you've already created the database.`
5. [[EFCore CRUD]] - Now that we've set up the database, here is how to CRUD it.
6.  [[Fluent API]] - When migrating code first, the model attributes automatically map into the Table, but the model attributes only cover a subset of the fluent API functionality, so there are mapping scenarios that cannot be achieved using annotations. This is where you can use Fluent API.
7. [[EF Table Relations]] - How to make Relations in Entity Framework Core. Primary Key, foreign key connections and all that.
8. [[EF Core Async]] - When dealing with websites and databases, of course you have to async them.

- [[EFCore Stored Procedure]] - learn this in case you might need it. Perform complex database operations with a single call. Can be used instead of LINQ.
# Questions:
- How to handle SQL injection attacks in Entity Framework?
	Entity Framework is injection safe since it always generates parameterized SQL commands which help to protect our database against SQL Injection. A SQL injection attack can be made in Entity SQL syntax by providing some malicious inputs that are used in a query and in parameter names. To avoid this one, you should never combine user inputs with Entity SQL command text.
- What are the various Entity States in EF?
	Each and every entity has a state during its lifecycle which is defined by an enum (EntityState) that have the following values:
	- Added
	- Modified
	- Deleted
	- Unchanged
	- Detached
- What are various approaches in Code First for model designing?
	There are two approaches, which you can use to define the model in EF Code First:
		- POCO model classes with data annotations
		- POCO model classes with FluentAPI in DbContext
	In Entity Framework Code First approach, our POCO classes are mapped to the database objects using a set of conventions defined in Entity Framework. If you do not want to follow these conventions while defining your POCO classes, or you want to change the way the conventions work then you can use the fluent API or data annotations to configure and to map your POCO classes to the database tables. 