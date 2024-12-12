How to to do CRUD in the database? simply inject the DbContext in a service, and let the service do some LINQ.
We will be using `ApplicationDbContext` from the previous samples. see: [[DbContext and DbSet]].
>[!warning] Important
>It might not be a good idea to directly **connect a Service to a database/Injecting a database to a Service**, It might be better to implement a [[Repository]]  also see: [[Inject Repository to Service]] if you already have one.
#### Injecting
```c#
public class SampleService : ISampleService
{
	private readonly ApplicationDbContext _db
	
	public SampleService(ApplicationDbContext applicationDbContext)
	{
		_db = applicationDbContext;
	}
}
```
The Service can use `_applicationDbContext` whatever the requirements need by using [[LINQ]].
For example:
```c#
//assuming this method is inside the service
public List<Person> GetPerson(string name)
{
	return _db.Persons.Where(person => person.Name == name);
	//Persons is a DbSet, which means a collection of Person type.
	//db is a DbContext.
}
```
`Persons` is the DbSet from the previous sample, dont be confused see: [[DbContext and DbSet]].
>[!warning]
>By Default, an EF core injection is singleton scoped, you might encounter a captive dependency if the DB is injected to a non singleton service. see: [[Best Practice for Services and DI]], see:[[Transient, Scoped, Singleton]].
##### Also take NOTE: 
That since you are dealing with a database and a website, it might be necessary to **async** the methods, see: [[EF Core Async]].
The samples above and below are not async. You will also async the action methods.
#### Create
To insert data to the DB we use:
```c#
//assuming this method is inside the service
public void AddPerson(Person person)
{
	_sb.Persons.Add(person);
	//also maybe add some linq validation in case there are duplicate persons
	_sb.SaveChanges();
}
```
>[!warning]
>This is just for sample, you rarely use void methods for crud of a service. You should consider passing [[DTO]]'s.
#### Delete:
```c#
public void DeletePerson(string name)
{
	Person PersonToDelete = _db.Persons.FirstOrDefault(person => person.Name == name);
	_db.Persons.Remove(PersonToDelete);
	_db.SaveChanges();
}
```
#### Update:
```c#
public void UpdatePersonName(string name, string newName)
{
	Person? matchingPerson = _db.Persons.FirstOrDefault(person => person.Name == name)
	matchingPerson.Name = newName;
	
	_db.SaveChanges();
	//if there are multiple updates on a single method, you only need one SaveChange()
}
```
#### Read
I think you know how to do a read. Just handle some `_db.Persons` like in the samples above.


>[!Warning]
>When Using DTO method inside a DB linq, it will not execute because it may cause memory leak.  
>This will usually happen when you are using a method inside Linq Select(). First transfer the data into a List by using Db.ToList() then do your select on the ToList, ToList().Select(etc..).
##### Again take NOTE: 
- That since you are dealing with a database and a website, it might be necessary to **async** the methods, see: [[EF Core Async]]. The samples above and below are not async. You will also async the action methods.
- It might not be a good idea to directly **connect a Service to a database/Injecting a database to a Service**, It might be better to implement a [[Repository]]  also see: [[Inject Repository to Service]] if you already have one.