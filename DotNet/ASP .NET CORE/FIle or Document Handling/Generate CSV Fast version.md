Generate Comma-separated value files.
# How-to:
First assuming we are using this model:
```c#
public class Person
{
    public int PersonId { get; set; }
    public string? Name { get; set; }
}
```
#### Service Method
Create a CSV generator method in your service that returns a `MemoryStream`, we will use `MemoryStream` since we're moving data to a file.
- **But first, In the service class library, nuget install "CsvHelper".**
Assuming we are using the previous Person Model, and writing this in the **`PersonService.cs`**.
sample:
```c#
public MemoryStream GetPersonCsvStream()
{
	MemoryStream memoryStream = new MemoryStream();
	using (StreamWriter streamWriter = new StreamWriter(memoryStream))
	{
		CsvWriter csvWriter = new CsvWriter(streamWriter, CultureInfo.InvariantCulture, leaveOpen: true);
		//InvariantCulture means the default text culture. It will be english.
		//leaveOpen means the stream doesnt close so we can continue to write.
		
		csvWriter.WriteHeader<Person>();
		//this will write the model properties as headers for the csv automatically.
		
		csvWriter.NextRecord(); //will add nextline in the csv
		
		List<Person> persons = //assume there is code here getting data from repository or DB
		csvWriter.WriteRecords(persons); //will loop through persons and write each in the csv.
		csvWriter.Flush(); //flush the temp data
	}
	
	// Create a new MemoryStream and copy the data from the original stream
	MemoryStream newMemoryStream = new MemoryStream(memoryStream.ToArray());
	
	//bring back the cursor to the beginning since we will need to read it again from the beginning later.
	memoryStream.Position = 0;
	
	return newMemoryStream;
}
```
#### Controller
in the action method:
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
This will download the csv file to the client.
>[!info]
>I don't need to mention this, but just in case you forget. You execute this by adding a route attribute to the action method and a link or a button on a view that leads to the action method, that link/button will be the download button and will automatically download the file to the client.
### The sample above is a fast and easy way to quickly generate a CSV
Each value cannot be customized or removed using the method above.
For a more detailed CSV generation see: [[Generate CSV Detailed version]].
>[!Warning]
>Since you are dealing with a database and a website, it might be necessary to **async** the methods, see: [[EF Core Async]] or [[Asynchronous Async]]. The samples above are non-async. Simply convert it to async.
The samples above and below are not async. You will also async the action methods.