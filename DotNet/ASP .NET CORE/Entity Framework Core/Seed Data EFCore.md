Data seeding is the process of populating a database with an initial set of data.
>[!question] Why?  
>Because you will need to set up a known data state for testing, development, or deploying an application for the first time
# How-To:
Assuming  you have mapped your models to the DB. If not see: [[DbContext and DbSet]].
#### Using Json Prebuilt
lets say you have the model Person:
```c#
internal class Person
{
	[Key]
	public int PersonId { get; set; }
	public string? Name { get; set; }
}
```

Then you create a Json containing pre built data for the Person model.
Lets say you have a json file named `people.json`:
```json
{
	"PersonId" : "89B1864C-47BE-4A7B-A2B0-7267C550EFF1",
	"Name" : "Johnny"
},
{
	"PersonId" : "9FDBEA1E-DAE9-4D8C-8B2E-F8B119411746",
	"Name" : "Cassie"
},
//more data
```
Store it in the main folder of the project, alongside appsettings.
#### Add Json Seed
To add `people.json` as the seed, 
on your `OnModelCreating` override method add:  (see:[[DbContext and DbSet]] if you forgot about `OnModelCreating`)
```c#
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);
    
	//read json file into string
    string peopleJson = System.IO.File.ReadAllText("people.json");
    
    //deserialize the string json into a list of the type
	List<Person> people = JsonSerializer.Deserialize<List<Person>>(peopleJson);
	
	foreach (var person in people) //for each value in the list
	{
		//generate a seed
	    modelBuilder.Entity<Person>().HasData(person); //this is the code that generate the seed
	}
}
```