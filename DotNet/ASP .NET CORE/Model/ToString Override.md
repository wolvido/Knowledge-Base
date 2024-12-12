---
keywords: |-
  name of the model returns
  name of the property returns
---
Represents the string value of the model.
```c#
public class Person
{
	public Guid PersonID { get; set; }
	public string? PersonName { get; set; }
	public string? Email { get; set; }
	public DateTime? DateOfBirth { get; set; }
	public string? Gender { get; set; }
	
	public override string ToString()
	{
		return $"Person ID: {PersonID}, Person Name: {PersonName}, Email: {Email}, Date of Birth:{DateOfBirth?.ToString("MM/dd/yyyy")}, Gender: {Gender}";
	}
}
```

An override for **`ToString`** of a model is used when the model is called by a method that expects a string return, 
because otherwise the model will return the name of the property, instead of the value of the property.
For example:
```c#
public async Task<List<Person>> GetAllPersons()
{
	var persons = await _personsRepository.GetAllPersons();
	
	_diagnosticContext.Set("Persons:", persons);
	
	return persons.Select(temp => temp.Person()).ToList();
}
```
###### Without **`override ToString`**, the diagnostic will return:
```json
["Entities.PersonID", "Entities.PersonName", "Entities.Email", "Entities.DateOfBirth", "Entities.Gender"]
```
###### With `ToString` it will return
```json
["PersonID: 231423534, Person Name: john, Email: @email.com, Date of Birth: 01/23/2032, Gender: gay-maybe"]
```
