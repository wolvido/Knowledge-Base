Sample test unit:
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
_personRepositoryMock.Setup(temp => 
								temp.AddPerson(It.IsAny<Person>() )
							)
							.ReturnsAsync(person);
```
This code says: When "`PersonsRepository.AddPerson`" is called, it has to return the same "person" object
- "`Setup()`" means we will setup one of the methods of the repository.
- "`repo => repo.AddPerson(...)`" means **`AddPerson()`** is  the method were setting up, and "`repo`" is just a lambda temporary for the repository.
- **`AddPerson()`** of the repository accepts a Person type, so "`It.IsAny<Person>()`" mocks any Person object as parameter.
- "**`.ReturnsAsync(person);`**" returns the person we created in the arrange section.
So essentially, you are telling repository mock that, as soon as someone calls `AddPerson()` repository method, it should accept a Person object, and return the Person object we made earlier.
###### This piece of code is taken from [[Mock Repository]], see that note for the full details.