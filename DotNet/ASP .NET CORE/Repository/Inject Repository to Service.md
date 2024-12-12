Instead of a service directly connecting to a database, Have the repository connect to the database through DcContext, and inject the repo to the service. See: [[Repository]] if confused.
```c#
public class PersonsService : IPersonsService
{
	//We Inject the Repository
	private readonly IPersonsRepository _personsRepository;
	public PersonsService(IPersonsRepository personsRepository)
	{
		_personsRepository = personsRepository;
	}
	
	//then use the repository CRUD methods
	public async Task AddPerson(Person? person)
	{
		//implement the AddPerson() of `PersonsRepository`
		await _personsRepository.AddPerson(person); 
			//so instead of the service accessing the DB directly, we access the repository instead
			//the db and the service is decoupled
	}
	
	public async Task<List<Person>> GetAllPersons()
	{
		//implement the GetAllPersons() of `PersonsRepository`
		var persons = await _personsRepository.GetAllPersons();
	}
	
	//other methods that will use the CRUD methods of the Repository
  {
}
```
#### Program.cs
Then in `program.cs` register your repository and repository interface, to inject accordingly:
```c#
builder.Services.AddScoped<IPersonsRepository, PersonsRepository>();
```
#### See:[[Repository]] if confused.