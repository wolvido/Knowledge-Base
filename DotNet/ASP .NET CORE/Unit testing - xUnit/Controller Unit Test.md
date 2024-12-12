Unit testing Controllers using x-unit.
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
- We are going to assume that we are using an Entity-based design, It means we design controllers based on the entities. see: [[Responsibilities of a Controller]].
- In this sample we'll assume we have a **`Persons.cs`** entity/model.
- Assuming we have a **`PersonsControllerTest.cs`** class in the test project, that tests the **`PersonsController`**.
- Assuming **`PersonsController`** uses a **`PersonsService`**.
	**Controllers are designed to be loosely coupled from the business logic aka services, so when testing the controller, we have to mock the service.**

In **`PersonsControllerTest`**, inject the mock of the service and all the tools.
```c#
 public class PersonsControllerTest
 {
	//field for the service used by the controller
	private readonly IPersonsService _personsService;
	//field for the mock service
	private readonly Mock<IPersonsService> _personsServiceMock;
	//Auto fixture, see AutoFixture note.
	private readonly Fixture _fixture;
	//the controller to be tested
	private readonly PersonsController _controller;
	
	public PersonsControllerTest()
	{
		//inject them all
		_fixture = new Fixture();
		_personsServiceMock = new Mock<IPersonsService>();
		_personsService = _personsServiceMock.Object;
		_controller = new PersonsController(_personsService);
			//initialize the controller on every test method, if you are using different services for every method
			//in this sample there is only one service
	}
	
	//test the action methods
	//[Fact]
	//etc...
}
```
###### Now we simply test the action methods using the mock service and the tools
- Lets assume we are testing the Index action method that returns a list of person to be displayed in the view.
- The Index action method calls the service method **`GetAllPersons()`**.
```c#
public async Task<IActionResult> Index()
{
	List<PersonResponse> persons = await _personsService.GetAllPersons();
		//it grabs the persons by using .GetAllPersons();
	
	return View(sortedPersons);
}
```
###### In order to test it we have to mock the service method used by the action method, as per best practices.
```c#
#region Index
[Fact]
public async Task Index_ShouldReturnIndexViewWithPersonsList()
{
	//Arrange
	List<person> persons_response_list = //assume there is mocking fixture code here
	
	//setup the mock GetAllPersons() that will be used by Index()
	_personsServiceMock
		.Setup(service => 
					service.GetAllPersons()
				)
		.ReturnsAsync(persons_response_list);
	
	//Act
	IActionResult result = await _controller.Index(); //run the index and grab it in result variable
	
	//Assert
	viewResult.ViewData.Model.Should().Be(persons_response_list);
		//the view data can contain the model data, 
		//here we assert that result model data was the same as the one arranged
}
#endregion
// dont confuse, this unit test is inside `PersonsControllerTest`
```
###### Moq Code Explanation
```c#
_personsServiceMock
	.Setup(service => 
				service.GetAllPersons()
			)
	.ReturnsAsync(persons_response_list);
```
- "`Setup()`" means we will setup one of the methods of the repository.
- "`service => service.GetAllPersons(...)`" means **`GetAllPersons()`** is  the method were setting up, and "`service`" is just a lambda temporary for the service.
- **`GetAllPersons()`** of the service accepts nothing, so the parameter is empty, some tests it might not be empty so refer to [[Moq code Explanation]] on how that works.
- "**`.ReturnsAsync(persons_response_list);`**" returns the persons list we created in the arrange section.
So essentially, you are telling the service mock that, as soon as someone calls `GetAllPersons()` service method, it should return the Persons list object we made earlier.
###### You don't need to use `_personsServiceMock` if the action method you are testing does not call a service method.
You can now Extrapolate how to mock any other action methods that uses other service methods, all you have to do is setup the proper parameter and the proper return.





