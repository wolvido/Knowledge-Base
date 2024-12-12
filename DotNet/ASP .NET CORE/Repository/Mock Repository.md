FIteFMock the repository for testing a service, so the service test is isolated. See [[Mocking]] if you forgot what mocking is.
![[Pasted image 20240219154821.png]]
# How-To:
- First, In your unit test project, nuget install **Moq**.
- Then in the same test projec, nuget install **EntityFrameworkCoreMock.Moq**.
These tools will make mocking easier in a project that uses [[Entity Framework Core]].
#### Mock Repository
Since we are mocking a repository, that means we are testing a service, since a service is the one that needs a repository.
- **Assuming you are testing a service that rely on a Repository**. 
- Assuming the service you are testing is called **`PersonsService`**, as the name suggests, it is a service for Person type.
- Assuming your repository is called **`PersonsRepository`** and its interface  **`IPersonsRepository`**
###### So in order to test the service, you created a Test Class named **`PersonsServiceTest`** that has a dependency on **`PersonsRepository`**:
```c#
//this is a test class, in a test project, testing a service, not a normal class or a service.
public class PersonsServiceTest
{
	//field for service and repo
	private readonly IPersonsService _personService;
	private readonly IPersonsRepository _personsRepository
	
	public PersonsServiceTest(IPersonsRepository personsRepository)
	{
		//directly inject the real repository
		_personsRepository = personsRepository;
		
		//Inject the repository into the service needing it
		var _personService = new PersonsService(_personsRepository);
			//this is direct dependency and is wrong
	}
	
	//codes testing the methods of PersonsService...
	//[Fact]
	//_personService.AddPerson(person)...
	//etc..
}
```
**This is wrong**; you created a dependency; this class test depends on a real repository. If the repo changes, the tests might also change.
###### So instead of injecting the Repo directly and creating a dependency, we can create a mock repository:
```c#
public class PersonsServiceTest
{
	private readonly IPersonsService _personService;
	//this will be used to configure mock data and create the mock object
	private readonly Mock<IPersonsRepository> _personRepositoryMock;
	//this is for the mocked object created by Mock<IPersonsRepository>
	private readonly IPersonsRepository _personsRepository;
	
	public PersonsServiceTest()
	{
		//inject the mocking
		_personRepositoryMock = new Mock<IPersonsRepository>();
		//create a mock repository object from Mock<IPersonsRepository>
		_personsRepository = _personRepositoryMock.Object;
		
		//inject the mock object to the service
		_personService = new PersonsService(_personsRepository);
	}
	
	//codes testing the methods of PersonsService while using the repo...
	//[Fact]
	//_personService.AddPerson(person)...
	//etc..
}
```
#### Testing the methods
inside the **`PersonsServiceTest`**, say we are testing the **`AddPerson()`** method of **`PersonsService`**", this method uses a repository method called **`AddPerson();`**. They are different but the same name, don't get confused.  **`AddPerson()`** of the service calls the  **`AddPerson()`** of the repository, which then adds something to the database.
Repository method:
```c#
public async Task AddPerson(Person person)
{
	//receives a person then adds that person in the database
	//returns a person type
}
//the method is an async version 
```
Service method:
```c#
public async Task<Person> AddPerson(Person? person)
{
	//accepts a Person type, then returns a Person type
	//calls AddPerson() of the respository and sends a person to that method
}
```
###### So:
- The **`AddPerson()`** service method calls the **`AddPerson()`** repository method. 
- **`AddPerson()`** repository method sends to the DB and returns Person type to the service.
So, to test the **`AddPerson()`** of the service method., first we need to setup the  **`AddPerson()`** of the repository method:
```c#
[Fact]
public async Task AddPerson_PersonNameIsNull_ToBeArgumentException() //testing the AddPerson of the service method
{
	//Arrange
	Person person = //assume there is a mock fixture here, see autofixture note
	
	//setup the repository method first before we act, this is where we use the _personRepositoryMock
	//When PersonsRepository.AddPerson is called,-
	//it has to return the same person object from the arrange above
	_personRepositoryMock.Setup(repo => repo.AddPerson(It.IsAny<Person>())).ReturnsAsync(person);
		//this whole code is part of the arrange
	
	//Act
	Func<Task> action = async () =>
	{
		await _personService.AddPerson(person);
			//inside .AddPerson(), .AddPerson() of the respository is also being called but mocked
	};
	
	//Assert
		//assume there is fixture Assert code here
}
//dont get confused, this test method is still inside PersonsServiceTest
```
###### Code Explanation:
```c#
_personRepositoryMock.Setup(repo => 
								repo.AddPerson(It.IsAny<Person>() )
							).ReturnsAsync(person);
```
This code says: When "`PersonsRepository.AddPerson`" is called, it has to return the same "person" object
- "`Setup()`" means we will setup one of the methods of the repository.
- "`repo => repo.AddPerson(...)`" means **`AddPerson()`** is  the method were setting up, and "`repo`" is just a lambda temporary for the repository.
- **`AddPerson()`** of the repository accepts a Person type, so "`It.IsAny<Person>()`" mocks any Person object as parameter.
- "**`.ReturnsAsync(person);`**" returns the person we created in the arrange section.
So essentially, you are telling repository mock that, as soon as someone calls `AddPerson()` repository method, it should accept a Person object, and return the Person object we made earlier.
###### **You don't need to use `_personRepositoryMock` if the test doesn't call a repository method.**
You can now Extrapolate how to mock any other repository methods in other service test methods, all you have to do is setup the proper parameter and the proper return.

>[!Warning] Important
>Anything new you inject in a repository, You will also need to mock, or error will ensue.
>In the constructor of the test, just create: 
>`var nameOfObject = new Mock<InterfaceOfTheType>():`
>and then inject it into the service, like the sample above.
