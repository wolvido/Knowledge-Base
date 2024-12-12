Unit testing a [[Services - Service layer]].
# How-To:
#### Installation:
First is installing tools, skip this if you've already installed.
###### Moq
In this sample we will use **EntityFrameworkCoreMock.Moq** and **Moq** Package.
- In your unit test project, nuget install **Moq**.
- Then in the same test projec, nuget install **EntityFrameworkCoreMock.Moq**.
These tools will make mocking easier in a project that uses [[Entity Framework Core]].
###### Auto Fixture
- Nuget Install AutoFixture in your Test Project, not the main project.
#### Testing
Assuming we are testing **`PersonsService.cs`** and the service uses a repository called **`PersonsRepository`**.
In your test project add **`PersonsServiceTest.cs`** class.
Simply create a test class named **`PersonsServiceTest`**:
```c#
public class PersonsServiceTest
{
	//field for injection of the service to be tested
	private readonly IPersonsService _personService;
	
	//repository mock, see "mock repository" note
	private readonly Mock<IPersonsRepository> _personRepositoryMock;
	private readonly IPersonsRepository _personsRepository;
	
	//output helper, see "ITestOutputHelper" note
	private readonly ITestOutputHelper _testOutputHelper;
	
	//Auto fixture, see "AutoFixture" note
	private readonly IFixture _fixture;
	
	//constructor
	public PersonsServiceTest(ITestOutputHelper testOutputHelper)
	{
		//inject Auto fixture
		_fixture = new Fixture();
		//Inject repo mock
		_personRepositoryMock = new Mock<IPersonsRepository>();
		_personsRepository = _personRepositoryMock.Object;
		//inject the service with the repo mock
		_personService = new PersonsService(_personsRepository);
		//inject the Output helper
		_testOutputHelper = testOutputHelper;
	}
	
	//Then simply test the methods
	[Fact]
	public async Task AddPerson_NullPerson_ToBeArgumentNullException()
	{
		//Act
		//act codes here...
		//Arrange
		//arrange codes here...
		//Assert
		//codes...
	}
	
	//[Fact]
	//etc...
```
Test the methods while using the techniques learned in [[Unit Testing - xUnit]].
Techniques such as:
-  [[Best Practices Unit tests]]
- [[Mocking]]
- [[AutoFixture]]
-  [[ITestOutputHelper]]
