While enrichment properties logs the same thing on every log message of every request, **IDiagnosticContext** will have a context for every request, which means it allows for dynamic log for each request. 
You can set the key-value pairs in the methods itself, and set the value of the log to whatever data the method uses. Instead of a static key-value pair.
# How-To:
Lets assume we are going to log the services.
- In your services project, nuget install **Serilog.Extensions.Hosting**.
###### Then inject it in your service
Lets assume you have a `PersonsService.cs`:
```c#
 public class PersonsService : IPersonsService
 {
	 private readonly IDiagnosticContext _diagnosticContext;
	 
	 public PersonsService(IDiagnosticContext diagnosticContext)
	 {
		 _diagnosticContext = diagnosticContext;
	 }
 }
```
Now your service has access to the Diagnostic Context.
###### Let's say your service has a method that gets all the person
```c#
public async Task<List<Person>> GetAllPersons()
{
	var persons = await _personsRepository.GetAllPersons();
	
	//In this method, you will of course want to log what persons the repository returned, so you add:
	_diagnosticContext.Set("Persons:", persons);
		//this will log the collection of persons
		//this is similar to the key-value pair of enrichment properties-
		//but this time, we set it in the code not the config, this makes it dynamic and code based.
	
	return persons.Select(temp => temp.Person()).ToList();
}
```
###### Now you can create meaningful logs that can help identify any problems.

Might need to remember this in case you get property name instead of property value: [[ToString Override]].
