Auto Fixture is a library that automates creating mock models/Entities with generated data.
It generates objects of the specified model/entity and their properties with some generated values based on their data types.
![[Pasted image 20240214145231.png]]
# How-To:
- Nuget Install AutoFixture in your Test Project, not the main project.
##### Test Class
- Assuming the service you are testing is called **`PersonsService`**, as the name suggests, it is a service for Person type.
- You created a **`PersonsServiceTest`** to test the **`PersonsService`**.
```c#
public class PersonsServiceTest 
{
	private readonly IPersonsService _personService;
	
	//Fixture field for injection
	private readonly IFixture _fixture;
	
	public PersonsServiceTest()
	{
		_fixture = new Fixture(); //this is the class that creates the mock objects
	
		//assume there is mocking codes here...
		//see mocking note if you get confused
		var dbContext = //assume we have already mocked this
		
		//assume there is mocking codes here...
		
		_personService = new PersonsService(dbContext);
	}
	
	//More codes below...
}
```
#### Fixture Create
So, after you have injected Fixture in the test class, You can us its `.Create` method to create mock objects in your test methods.
sample:
```c#
//this test method is inside the PersonsServiceTest class
[Fact]
public void AddPerson_AddPersonTest()
{
	//Arrange
	Person person = _fixture.Create<Person>(); //use _fixture.Create to create dummy values for a person type
	
	//Act
	AddPerson(person);
	Person? personFromDb = //assume there is code here taking the newly added person from the DB
	
	//Assert
	Assert.Equal(personFromDb, person);
}
```
#### Fixture Build
Instead of `_fixture.Create` you can use **`_fixture.Build`** for more fine grained control of the mock data, it will allow you to override and customize some values when needed.
###### For example, lets say your model has an `Email` property with validation
```c#
public class Person
{
    public int PersonId { get; set; }
    
    [EmailAddress(ErrorMessage = "{0} Invalid, enter a valid {0}")]
    public string? Email { get; set; }
}
```
If we use **`_fixture.Create`** it will generate a default email that is `Email0335e58b-be62-4811-869b-3de41ff6d00d` the validation will not accept and will flag that as an error. To prevent that we can specify the email using `_fixture.Build.` and `.With` .
sample:
```c#
[Fact]
public void AddPerson_AddPersonTest()
{
	//Arrange
	Person person = _fixture.Build<Person>()
		.With(person => person.Email, "valid@email.com") //will replace the default email generated into "valid@email.com"
		.Create(); //then we call create to set default random data on the rest of the properties
		//the other properties will still generate random data
	
	//Act
	AddPerson(person);
	Person? personFromDb = //assume there is code here taking the newly added person from the DB
	
	//Assert
	Assert.Equal(personFromDb, person);
}
```
![[Pasted image 20240214174659.png]]