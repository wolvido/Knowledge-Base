The Repository Pattern is used to separate the logic that retrieves data from the underlying storage (such as a database) from the rest of the application. Essentially, instead of tightly coupling your program to the database, you will use the repository as intermediary and decouple the DB. It's essentially the controller of Infrastructure.
![[Pasted image 20240215150230.png]]
#### How it works?
In the repository you will implement the CRUD methods that might be needed by the service that will access the repository, so that the DB is separated from the business logic. The services will not access the database at all.

So, for example lets assume we have a **`PersonService.cs`** that handles the business logic related to the **`Person`** model/entity.
###### We implement a generic repository that will handle the crud of **`PersonService.cs`** , call it `PersonsRepository`.
Here is its Interface:
```c#
public interface IPersonsRepository
{
	Task AddPerson(Person person);
	
	Task<Person> GetPersonById(Guid personId);
	
	Task<List<Person>> GetAllPersons();
	
	//...Delete, Update, etc..
}
```
###### Then, in the **`PersonService.cs`**, we will use the CRUD methods of `PersonsRepository`:
```c#
public class PersonsService : IPersonsService
{
	//We Inject the Repository
	private readonly IPersonsRepository _personsRepository;
	public PersonsService(IPersonsRepository personsRepository)
	{
		_personsRepository = personsRepository;
	}
	
	//then from our previous repository implementation, use the repository CRUD methods
	public async Task AddPerson(Person? person)
	{
		//implement the Add of `PersonsRepository`
		await _personsRepository.AddPerson(person);
			//so instead of the service accessing the DB directly, we access the repository instead
			//the db and the service is decoupled
	}
	
	public async Task<List<Person>> GetAllPersons()
	{
		//implement the GetAll of `PersonsRepository`
		var persons = await _personsRepository.GetAllPersons();
	}
	//other methods that will use the CRUD methods of the Repository
		//[Fact]
		//_personsRepository.GetAllPersons()...
}
```
The Service will **not need to access the DbContext** as such will not access the Database, essentially creating a separation.
# How-To:
- Just like in services, Create two new class library.
-  name one as "RepositoryContracts" (contracts means interfaces).
- name the other as "Repositories".
Now you have two class libraries.
**NOTE:** If you are using [[Clean Architecture]], you put the repository classes in the "Repositories" folder inside [[Infrastructure Layer]] and the "RepositoryContracts" in the domain folder.
#### Repository Contracts
- So, assuming we are using the **`Person`** model/entity and **`PersonService`**.
- In your "RepositoryContracts" class library, create the the **`IPersonsRepository.cs`**.
In the **`IPersonsRepository.cs`**, create the CRUD interface methods just like the sample above:
```c#
public interface IPersonsRepository
{
	Task AddPerson(Person person);
	
	Task<Person> GetPersonById(Guid personId);
	
	Task<List<Person> > GetAllPersons();
	
	//...Delete, Update, etc..
}
```
The methods here are CRUD methods that will be needed by the service that will access the repository.
>[!info] Important
>The CRUD methods in a repository might not necessarily be generic CRUD methods, they might be more specialized depending on the specification and requirements of the team. You might need to creare more specialized CRUD methods like:
>`public Person? GetPersonByPersonID(Guid personID)`.
#### Repository Implementation
Then, Implement the interface and its methods, into a repository.
- Inside "Repositories" class library, create a **`PersonsRepository.cs`** class.
- Then simply inherit from the interface, and implement it.
```c#
public class PersonsRepository : IPersonsRepository
{
	//Inject the DB
	private readonly ApplicationDbContext _db;
		//ApplicationDbContext is the name of the DbContext in this sample
	public PersonsRepository(ApplicationDbContext db)
	{
		_db = db; //injection
	}
	
	public async Task AddPerson(Person person) //Implement AddPerson()
	{
		_db.Add(person);
		await _db.SaveChangesAsync();
	}
	
	public async Task<Person?> GetPersonById(Guid personId) //Implement GetPersonById()
	{
		return await _db.Persons.FirstOrDefaultAsync(person => person.PersonID == personID);
	}
	
	public async Task<List<Person>> GetAllPersons() //Implement GetAllPersons()
	{
		return await _db.Persons.ToListAsync();
	}
}
```
>[!info]
>The commands are [[LINQ]].
#### Program.cs
Then in `program.cs` register your repository and repository interface, to inject accordingly:
```c#
builder.Services.AddScoped<IPersonsRepository, PersonsRepository>();
```
# What next?
- since this is an intermediary between Business Logic and Database, how do we connect the Services to the Repositories? Just like the sample above, simply inject it see: [[Inject Repository to Service]].
- Mock the repository for testing: [[Mock Repository]].