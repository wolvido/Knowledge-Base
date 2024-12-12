see: [[Generate Excel]] for some context.
# How-To:
Assuming were using this model:
```c#
public class Person
{
	public string? Name { get; set; }
	public string? Email { get; set; }
}
```
#### Service
- First, in your service library, nuget install: **"Microsoft.AspNetCore.Http**".
Then, In your service that handles `Person` add the method:
```c#
int UploadPersonsExcel(IFormFile formFile) //return type is int so we can show the number of Persons uploaded
{
	//convert the file back to memory stream
	MemoryStream memoryStream = new MemoryStream();
	formFile.CopyTo(memoryStream);
	
	//count the number of Person inserted
	int personsInserted = 0;
	
	using (ExcelPackage excelPackage = new ExcelPackage(memoryStream))
	{
		ExcelWorksheet workSheet = excelPackage.Workbook.Worksheets["Persons"]; 
			//"Persons" is name of the pre-built sheet
		
		//to get the number of rows filled by the user
		int rowCount = workSheet.Dimension.Rows;
		
		for (int row = 2; row <= rowCount; row++) //row starts with 2 because 1 are the headers
		{
			//grab the value of the current loop row in column 1 Name
			string? cellValueName = Convert.ToString(workSheet.Cells[row, 1].Value);
			//grab the value of the current loop row in column 2 Email
			string? cellValueEmail = Convert.ToString(workSheet.Cells[row, 2].Value);
			//add more headers/columns as necessary, depeding on requirements
			
			//if cellValues is not null
			if (!string.IsNullOrEmpty(cellValueName) && !string.IsNullOrEmpty(cellValueEmail))
			{
				string? name = cellValueName;
				string? email = cellValueEmail;
				
				//check if the person already exists in the db
				bool checkNoExistingPersons = _db.Persons
					.Where(person => person.Name == name)
					.Where(person => person.Email == email)
					.Count() == 0;
					
				if(checkNoExistingPersons) //if values does not exist, proceed with upload
				{
					//create the Persn object to be added with the provided data
					Person person = new Person()
					{
						Name = name,
						Email = email
					}
					//add and save the upload
					_db.Persons.Add(person);
					_db.SaveChanges();
						//note: we used _db, can be a repository if there is a repository, either way the same principl 
					
					personsInserted++;
				}
					//it might be necessary to create more validations.
					//It only checks for duplication, it does not check for wrong data in the excel file.
			}
		}
		return personsInserted;
	}
}
```
>[!warning] Be careful with this method
>- it might be necessary to create more validations. 
>- It assumes that the excel file to be uploaded has the exact mount of header and that it provides the correct data in the correct arrangement. 
>- It only checks for duplication, it does not check for wrong data in the excel file.
#### View
This notes assumes you know how to set up the view for a file, if not see:[[form-urlencoded and form-data]].
sample:
```html
<form asp-action="UploadFromExcel" asp-controller="SampleController" method="post" enctype="multipart/form-data">
	<input type="file" name="excelFile"/> //the `name="excelFile"` is important later on in the backend dont forget.
	<button type="submit"></button>
</form>
```
#### Controller
in your action method that handles the service:
```c#
//make sure the parameter name is the same as the <input> name, in the view sample we used excelFile
public IActionResult UploadFromExcel(IFormFile excelFile)
{
	//validations
	if (excelFile == null || excelFile.Length == 0) //check if there is a file
	{
		//store the error on the viewbag and display it later
		ViewBag.ErrorMessage = "Please add an excel file...";
		return View(); //return to the same view with the error
	}
	//check if it is an excel file
	if (!Path.GetExtension(excelFile.FileName).Equals(".xlsx", StringComparison.OrdinalIgnoreCase))
	{
		ViewBag.ErrorMessage = "Unsupported file. Please add an excel file...";
		return View();
	}
	//if all validations are passed, the we will use the service method
	int personsCountUploaded = _personService.UploadPersonsExcel(excelFile);
	ViewBag.Message = $"{personsCountUploaded} Persons uploaded";
	return View();
}
```

>[!Warning]
>Since you are dealing with a database and a website, it might be necessary to **async** the methods, see: [[EF Core Async]] or [[Asynchronous Async]]. The samples above are non-async. Simply convert it to async.
The samples above and below are not async. You will also async the action methods.