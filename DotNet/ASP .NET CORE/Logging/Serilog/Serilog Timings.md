To log the execution time of a piece of code. 
Usually used to know which piece of code is slowing down the program.
# How-To:
First, in the project you want to log to; nuget install **SerilogTimings**.
#### Timings
Lets say you have a `Service` and this service has a method called **`GetFilteredPersons()`** that is somewhat lengthy:
```c#
public async Task<List<PersonResponse>> GetFilteredPersons(string searchBy, string? searchString)
{
	List<Person> persons = null;
	
	//notice the code below is calling a repo and quite complicated, 
	//which means it might be accessing the database a lot, which might take long time of execution,
	//this is where we will use Serilog Timings using Operation.Time() and encase the code with `using`.
	using (Operation.Time("execution time of GetFilteredPersons accessing the database"))
	{ //beginning of timing
		persons = searchBy switch
		{
			nameof(PersonResponse.PersonName) =>
			 await _personsRepository.GetFilteredPersons(temp =>
			 temp.PersonName.Contains(searchString)),
			
			nameof(PersonResponse.Email) =>
			 await _personsRepository.GetFilteredPersons(temp =>
			 temp.Email.Contains(searchString)),
			
			nameof(PersonResponse.DateOfBirth) =>
			 await _personsRepository.GetFilteredPersons(temp =>
			 temp.DateOfBirth.Value.ToString("dd MMMM yyyy").Contains(searchString)),
			
			nameof(PersonResponse.Gender) =>
			 await _personsRepository.GetFilteredPersons(temp =>
			 temp.Gender.Contains(searchString)),
			
			nameof(PersonResponse.CountryID) =>
			 await _personsRepository.GetFilteredPersons(temp =>
			 temp.Country.CountryName.Contains(searchString)),
			
			nameof(PersonResponse.Address) =>
			await _personsRepository.GetFilteredPersons(temp =>
			temp.Address.Contains(searchString)),
			
			_ => await _personsRepository.GetAllPersons()
		};
	} //end of timing
	
	return persons.Select(temp => temp.ToPersonResponse()).ToList();
}
```
