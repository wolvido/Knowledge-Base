 When migrating code first, the model attributes automatically map into the Table, but the model attributes only cover a subset of the fluent API functionality, so there are mapping scenarios that cannot be achieved using annotations.
 This is where you can use Fluent API.
 Fluent API is a set of predefined methods in entity framework that allows you to specify more details on a column data type.
 For example you have the model:
```c#
 public class Person
{
	[Key] //means main key
	public int PersonId { get; set; }
	[StringLength(40)]
	public string? Name { get; set; }
	//Address property has no attributes applied
	public string? Address {get; set;}
}
```
If **`Name`** is migrated it will have the constraint of **`nvarchar 40`**. 
If **`Address`** property is migrated it will be generated as **`nvarchar max`** which will give a very bad performance for the DB.
###### Assuming the table already exists, add some constraint to a property using Fluent API
Inside the OnModelCreating method, that is inside your DbContext:
```c#
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
	base.OnModelCreating(modelBuilder) //to construct the parent class
	
	modelBuilder.Entity<Person>().Property(person => person.Address)
		.HasColumnType("nvarchar(200)"), //limits the characters to 200
		//you can also chain other methods
		.HasDefaultValue("new york city boulevard whatever")
		.HasColumnName("FullAddress"); //changes the name
}
```
- `modelBuilder.Entity<Person>() `returns an object that can be used to edit an entity that handles the `<generic>` type, in this case the generic is Person type. It tells EF Core that you are going to configure the mapping for the "Person" entity.
- Once you have the `<Person>` entity, you then add `.Property(person => person.Address)` to return a property of the Person type. `person => person.Address` specifies the property to be 'Address'.
- Then once you have `Address`,  `.HasColumnType("nvarchar(200)");` will add the constraint "nvarchar(200)" to the Address column in your DB.
>[!note]
>Do not confuse the `Has` method, it is not a condition of an existence of something. 
>It is a Setter method. Has simply means that you are specifying the column type that the property should have in the database. In the case of the sample above, `Address` property should has/have "nvarchar(200)" as a constraint. 

>[!question]- But why "has" though, isn't that confusing?
>well because thats the language in a database, read all of [[EF Table Relations]] for it to make sense.
###### Then run `Add-Migration Address_Updated` and `Update-Database` to implement the changes. 
see: [[Code-First Migrations]] if you don't know what that means.
#### Syntax of the code above:
![[Pasted image 20240131154217.png]]
See: [Fluent API - Configuring and Mapping Properties and Types - EF6 | Microsoft Learn](https://learn.microsoft.com/en-us/ef/ef6/modeling/code-first/fluent/types-and-properties) For a complete list and guide of all the configuring setter methods.
#### Configuring a whole table
Above we configured a property, here is sample of configuring the whole table:
```c#
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
	base.OnModelCreating(modelBuilder) //to construct the parent class
	
	modelBuilder.Entity<Person>().ToTable("Persons"); 
}
```
- Persons is the name of the table.
- `modelBuilder.Entity<Person>()` returns an object that can be used to edit an entity that handles the `<generic>` type, in this case `<Person>` type.
- Essentially tells EF Core that you are going to configure the mapping for the "Person" entity.
- Once you have the Person entity `.ToTable("Persons");` then maps the Person to a DB Table named Persons.
#### Syntax
![[Pasted image 20240131153043.png]]
Again, See: [Fluent API - Configuring and Mapping Properties and Types - EF6 | Microsoft Learn](https://learn.microsoft.com/en-us/ef/ef6/modeling/code-first/fluent/types-and-properties) For a complete list and guide of all the configuring setter methods.
#### Also see this
![[Pasted image 20240131164219.png]]
###### `IsUnique()` Sample:
```c#
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
	base.OnModelCreating(modelBuilder) //to construct the parent class
	
	modelBuilder.Entity<Person>()
		.HasIndex(p => p.Address).IsUnique();
}
```
- `.HasIndex(p => p.Address)` indicates that you want to create an index on the "Address" property of the "Person" entity.
- `.IsUnique()` specifies that the index should enforce uniqueness, meaning that no two entities can have the same email.
- It is similar to a primary key index but doesn't necessarily require the column to be the primary key, just that it should be unique.
#### `HasCheckConstraint()` sample:
```c#
modelBuilder.Entity<Person>()
    .Property(p => p.Age)
    .HasCheckConstraint("CHK_Person_Age", "[Age] >= 0");
```
Essentially an validation check, will return an exception if age if it receives age less than 0.

**Again**, See: [Fluent API - Configuring and Mapping Properties and Types - EF6 | Microsoft Learn](https://learn.microsoft.com/en-us/ef/ef6/modeling/code-first/fluent/types-and-properties) For a complete list and guide of all the configuring setter methods. This note is simply to familiarize.
