Integration test is to test how well all the layers/components integrate with each other. Essentially the opposite of unit test.
You're testing the whole stack instead of per unit.
>[!info] Note
>Harsha makes his integration tests to every route, but sometimes it might depend on the plan determined by the team. 
>As long as it tests the interactions and collaborations between different components or modules within your application, then it is considered an integration test.

In general, integration testing means you test every route in the controller, you test all outcomes when the client calls the route. Similar to unit testing where you test all outcomes when using the method.
# How-To:
>This is going to be a long how-to
#### Installation and File:
###### Mvc Testing
- In your unit test project, nuget install **Microsoft.AspNetCore.Mvc.Testing**.
###### EF Core InMemory
- In your unit test project, nuget install **Microsoft.EntityFrameworkCore.InMemory**.
###### Moq
In this sample we will use **EntityFrameworkCoreMock.Moq** and **Moq** Package.
- In your unit test project, nuget install **Moq**.
- Then in the same test projec, nuget install **EntityFrameworkCoreMock.Moq**.
These tools will make mocking easier in a project that uses [[Entity Framework Core]].
###### Auto Fixture
- Nuget Install AutoFixture in your Test Project, not the main project.
###### File
Since we are testing routes in a controller, we will group the routes by its controller, so create a **`PersonsControllerIntegrationTest.cs`** in your test project.
###### Naming
Post-fix the name of the integration test class with `IntegrationTest`.
#### Pre-requisites
###### First, in your "Program.cs", at the bottommost add this code:
```c#
public partial class Program {}
```
###### Then, edit the project file to include the test project in the item group
- right click on the project that contains `Program.cs`.
- click edit project file.
Then you will see:
```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
 
  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
	etc...
  </PropertyGroup>
 
  <ItemGroup>
    <ProjectReference Include="...csproj" />
    etc...
  </ItemGroup>
 
</Project>
```
Add another **`<ItemGroup>`** inside the **`</Project>`**:
```xml
<ItemGroup>
	<InternalsVisibleTo Include="NameOfTestProject" />
</ItemGroup>
```
save the file.
###### This will make the program class accessible to the test project when mocking a web application.
#### Third Party framework dependency
In case you program installed a third party frameworks such as Rotativa or anything else. You will need to disable them in program.cs. 
For example you have registered Rotativa in Program.cs:
```c#
//this is in program.cs
Rotativa.AspNetCore.RotativaConfiguration.Setup("wwwroot", wkhtmltopdfRelativePath: "Rotativa");
```
It needs to be disabled in testing environment:
```c#
//do this
if (builder.Environment.IsEnvironment("EnvironmentName") == false)
	Rotativa.AspNetCore.RotativaConfiguration.Setup("wwwroot", wkhtmltopdfRelativePath: "Rotativa");
```
###### **MAKE SURE** `"EnvironmentName"` is the same name in your **`WebApplicationFactory`**.
#### WebApplicationFactory
Since integration test require testing the whole application, we will need a server, a client, and a database.
We will use **`WebApplicationFactory`** to create and configure a separate test server, aka a "mock server" (see [[How Kestrel and other servers work]]), a "mock database", and a "mock client". **Not exactly a mock but, essentially a test environment.**
It will essentially make us a whole test environment, for testing.
###### In your test project add a **`CustomWebApplicationFactory.cs`**:
```c#
public class CustomWebApplicationFactory : WebApplicationFactory<Program> //this is where partial class program is imprted
{
	//here we configure the webhost
	protected override void ConfigureWebHost(IWebHostBuilder webHostbuilder)
	{
		base.ConfigureWebHost(webHostbuilder); //inherit from base
		
		webHostbuilder.UseEnvironment("EnvironmentName"); //dont forget to change this
		
		//obviously we cant use the real database in testing-
		//so we will delete the real memory in this testing environment-
		//and then configure the "mock webhost" to use an in-memory database.
		webHostbuilder.ConfigureServices(services => {
			var descriptor= services.SingleOrDefault(
				temp => temp.ServiceType == typeof(DbContextOptions<NameOfDbContext>)
			); //this code essentially finds the connected database of `NameOfDbContext`
			//`NameOfDbContext` is the DB context this app is using
			
			//if we find the database, we will delete it in this test environment.
			//because ofcourse we cant use the real DB in the testing
			if (descriptor != null) 
			{
				services.Remove(descriptor);
			}
			
			//Then here we create a new in-memory database, essentially a "mock DB" in temporary memory.
			services.AddDbContext<NameOfDbContext>(options =>
			{
				options.UseInMemoryDatabase("MockDatabaseForTesting");
			});
		});
	}
}
```
All the services lifecycle don't need to be configured, it was already copied from **`program.cs`**, through the **`WebApplicationFactory<Program>`**.
#### Testing
Now we've set up the test environment, we go to testing.
In general, integration testing means you test every route in the controller, you test all outcomes when the client calls the route.
But that is in general, there might be teams where they have different styles of testing.
- In this note we will do integration test per route of a controller.
- We will assume we are testing the routes of a controller named **`PersonsController`**.
- This is similar to a [[Controller Unit Test]] but instead of testing the if the action methods are correct, we are testing if the routes are correct.
Here we test the route to the **`"Persons/Index"`** of the page and check if the return is correct:
```c#
public class PersonsControllerIntegrationTest : IClassFixture<CustomWebApplicationFactory>
	//IClassFixture<CustomWebApplicationFactory> is where our CustomWebApplicationFactory is connected
{
	//field for our "mock client", not really a mock but a "mock" in essence
	private readonly HttpClient _httpClient;
	
	public PersonsControllerIntegrationTest(CustomWebApplicationFactory webApplicationFactory)
	{
		//we create the "mock client" using our webApplicationFactory
		_client = webApplicationFactory.CreateClient();
	}
	
	[Fact]
	public async Task Index_ToReturnView()
	{
		//Arrange
		//we already arranged it above and beyond above.
		
		//Act
		//simulate the client sending a http request to the route, then getting the response
		HttpResponseMessage response = await _client.GetAsync("Persons/Index");
		
		//Assert
		//check if response returns success
		response.Should().BeSuccessful();
	}
}
```
>[!warning] Important
>in some cases, the project might not use asynchronous action methods, in this sample we used asynchronous.
>convert it to non-async when necesssary.
# Integration testing with response body.]
X-Unit has no built in feature to test the html DOM that was returned with the html response, in order to test the html DOM we have to install a third party package called fizzler.
- in your test project, nuget install **Fizzler**.
- and also **Fizzler.Systems.HtmlAgilityPack**.
Then in your test case:
```c#
[Fact]
public async Task Index_ToReturnView()
{
	//Arrange
	//we already arranged it above and beyond above.
	
	//Act
	HttpResponseMessage response = await _client.GetAsync("Persons/Index");
	
	//Assert
	response.Should().BeSuccessful();
	
	//convert the response body as string
	string responseBody = await response.Content.ReadAsStringAsync();
	
	//create an html document object aka an empty DOM
	HtmlDocument html = new HtmlDocument();
	
	//then load the responseBody to the empty DOM to create the DOM of the response
	html.LoadHtml(responseBody);
	var document = html.DocumentNode;
	
	//document is the DOM, you can execute javascript code on it to test what you need
	document.QuerySelectorAll("table.persons").Should().NotBeNull();
		//QuerySelectorAll() is a javascript code it-
		//selects all element that has table class with persons class, see "js how to get an element" note if youre confused
		//Should().NotBeNull(); is fixture meaning we assert that "table.persons" element not be null
}
```
>[!warning]
>there is a known bug where in memory database has an error when seeding data. see https://www.udemy.com/course/asp-net-core-true-ultimate-guide-real-project/learn/lecture/34524546#questions/20405190 in questions for some info.