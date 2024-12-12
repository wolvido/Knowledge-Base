---
keywords: how to test a service with a database
---
As per the best practices of Unit Test cases. A Unit should be isolated, it should not depend on outside sources, no other classes, services, or database must be accessed in testing. 
In order to test without accessing dependencies, we must Mock the dependencies.
# How-To:
#### Test Double
A test double is an object that look and behaves like their production equivalent objects.
![[Capture 45.png]]
###### There are two types of Test Doubles: Fake and Mock.
**Fake** - A copied full object with copied methods and properties; similar to the real one, but in a simplistic reduced capacity; e.g. a fake web service.
**Mock** - Has no Implementation, simply returns a fixed return value for each property or method.
###### One type of dependency is the DbContext.
>[!Warning] Important
>Mocking DbContext is only used in very unique circumstance when the project doesn't use a repository. In most cases you **DO NOT MOCK THE DB CONTEXT**, you mock the repository instead [[Mock Repository]]. This is just a sample on how to mock a DbContext.
## Mocking a DbContext
##### Moq
In this sample we will use **EntityFrameworkCoreMock.Moq** and **Moq** Package.
- In your unit test project, nuget install **Moq**.
- Then in the same test projec, nuget install **EntityFrameworkCoreMock.Moq**.
These tools will make mocking easier in a project that uses [[Entity Framework Core]].
##### Mock DbContext
- **Assuming you are testing services that rely on a Database / DbContext**. 
- Also assuming the DbContext needed is **`ApplicationDbContext`** in [[DbContext and DbSet]].
- The service you are testing is called **`PersonsService`**, as the name suggests, it is a service for Person type.
- **`PersonsService`** uses a database, which is the **`ApplicationDbContext`**. (see: [[EFCore CRUD]] if youre confused ).
So in order to test the service, you created a **`PersonsServiceTest`** that has a dependency on **`ApplicationDbContext`**, and by extension has a dependency on a database:
```c#
//this is a test class, in a test project, testing a service, not a normal class or a service.
public class PersonsServiceTest
{
	//field for the service
	private readonly IPersonsService _personService;
	
	public PersonsServiceTest()
	{
		//directly call the DbContext
		var dbContext = new ApplicationDbContext(new DbContetOptionsBuilder<ApplicationDbContext>().Options);
		//Inject the DbContext into the service needing it
		var _personService = new PersonsService(dbContext);
			//this is direct dependency and is wrong
	}
	
	//codes testing the methods of PersonsService...
	//[Fact]
	//_personService.AddPerson(person)...
	//etc..
}
```
**This is wrong**; you created a dependency; this class test depends on a DbContext/Database. If the database changes, the tests might also change.
###### So instead of injecting the DbContext directly and creating a dependency, we can create a DbContext mock:
```c#
public class PersonsServiceTest 
{
	//field for the service
	private readonly IPersonsService _personService;
	
	public PersonsServiceTest()
	{
		//empty collection as mock data for the DbSet
		var personsInitialData = new List<Person>() {};
			// empty by default, but you can add initial seed data if necessary
			// person is not based on PersonService its a DbSet of ApplicationDbContext-
			//see "DbContext and DbSet" note if youre confused.
			
		//another empty collection for the other DbSet of ApplicationDbContext
		var ModelSampleInitialData = new List<ModelSample>() {};
		
		//create a mock for the DbContext
		DbContextMock<ApplicationDbContext> dbContextMock = new DbContextMock<ApplicationDbContext>(
		   new DbContextOptionsBuilder<ApplicationDbContext>().Options
		); 
			//The DbContextOptions is there because by default DbContexts are supplied with DbContextOptions for config
			//see "DbContext and DbSet" note for more details.
		
		// now we use dbContextMock to create a dbContext mock object.
		var dbContext = dbContextMock.Object;
			//now we have a mock DbContext that PersonsService can use for the test
		
		//Now we have to mock the DbSets of ApplicationDbContext, see "DbContext and DbSet" note if confused.
		dbContextMock.CreateDbSetMock(temp => temp.Persons, personsInitialData); 
		dbContextMock.CreateDbSetMock(temp => temp.ModelSamples, personsInitialData);
			//now we also have the DbSets ready to use
			
		//Simply Inject the mock DbSet
		_personService = new PersonsService(dbContext);
	}
	
	//codes testing the methods of PersonsService...
		//[Fact]
		//_personService.AddPerson(person)...
		//etc..
}
```
>[!Warning] Important
>It's not just the DbContext, Anything you inject in a service is a dependency, which will also need to be mocked, or error will ensue.
>In the constructor of the test, just create: 
>`var nameOfObject = new Mock<InterfaceOfTheType>():`
>and then inject it into the service, like the sample above.
# What next?
- How do we mock the model objects? see [[AutoFixture]]
- Mocking DbContext is only used in very unique circumstance when the project doesn't use a repository. In most cases you **DO NOT MOCK THE DB CONTEXT**, you mock the repository instead [[Mock Repository]].

