It works the same way as [[Generate CSV Fast version]] but in this version we need to add an object of `CsvCConfiguration` in order to configure the csv and the values. You will be able to edit the values or remove some values.

Assuming we are using the previous Person Model, and writing this in the **`PersonService.cs`**.
```c#
public MemoryStream GetPersonCsvStream()
{
	MemoryStream memoryStream = new MemoryStream();
	using (StreamWriter streamWriter = new StreamWriter(memoryStream))
	{
		//add CsvCConfiguration
		CsvConfiguration csvConfiguration = new CsvConfiguration(CultureInfo.InvariantCulture);
		//InvariantCulture means the default text culture. It will be english.
		
		CsvWriter csvWriter = new CsvWriter(streamWriter, csvConfiguration);
		
		//manually write the headers using WriteField() instead of WriteHeader()
		csvWriter.WriteField(nameof(Person.Id));
		csvWriter.WriteField(nameof(Person.Name));
		csvWriter.NextRecord(); 
		
		List<Person> persons = //assume there is code here getting data from repository or DB
		
		//write all the values for loop style
		foreach (Person person in persons)
		{
			//in this for loop is where you can costumize the values
			//you can add logic here depending on your requirement, for example you can shorten the name to only first
			//you can also remove a property, you can exclude person.Id if you want only the name
			csvWriter.WriteField(person.Id);
			csvWriter.WriteField(person.Name);
			csvWriter.NextRecord(); //next line
			csvWriter.Flush(); //flush for every line
		}
	}
	MemoryStream newMemoryStream = new MemoryStream(memoryStream.ToArray());
	memoryStream.Position = 0;
	
	return newMemoryStream;
}
```
#### Controller
in the action method, it is the same as the fast version.
```c#
public IActionResult PersonsCsv()
{
	MemoryStream memoryStream = _personService.GetPersonCsvStream(); //grab the stream from the method
	
	//Then return the the CSV stream as a downloadable file
	return File(memoryStream, "application/octet-stream", "persons.csv");
	//second parameter is the mime type of csv
	//third parameter is name of the file
	//see note FileResult for more detalye
}
```
>[!Warning]
>Since you are dealing with a database and a website, it might be necessary to **async** the methods, see: [[EF Core Async]] or [[Asynchronous Async]]. The samples above are non-async. Simply convert it to async.
The samples above and below are not async. You will also async the action methods.

