This note assumes you know how excel sheets work, the one with cells in address A1, B1, etc.. 
Don't get confused if you see A1, B1, C2 in the code.
# How-To:
First, assuming we are using this model:
```c#
public class Person
{
	public int PersonId { get; set; }
	public string? Name { get; set; }
}
```
#### Install
- nuget install EPPlus on your service library, not the main project.
- you also have to configure EPP for non-commercial use, If you are using for non-commercial. In appsettings add:
 ```json
"EPPlus":	{
	"ExcelPackage":
	{
		"LicenseContext": "NonCommercial"
	}
}
```
#### Service Method
Create a Excel generator method in your service that returns a `MemoryStream`, we will use `MemoryStream` since we're moving data to a file. 
Assuming we are writing this in a service that handles `Person` model.
```c#
MemoryStream GetPersonExcelStream()
{
    MemoryStream memoryStream = new MemoryStream();
    using (ExcelPackage excelPackage = new Excelpackage(memoryStream)) 
    {
        //create an empty workbook with an empty worksheet
        ExcelWorksheet workSheet = excelPackage.Workbook.Worksheets.Add("PersonsSheet");
	        //"PersonSheet" is the name of the sheet
        
        //to assign a value at cell A1
        workSheet.Cells["A1"].Value = nameof(Person.PersonId);
        //to assign a value at cell B1
        workSheet.Cells["B1"].Value = nameof(Person.Name);
	        //assigning cells manually like this would be tedious of course, this is for header only.
	        //use logic instead when assigning the values, maybe a foreach, depending on what you need.
	        
	    //excel styles. Refer to EPPlus documentation for more detailed styles
	    using (ExcelRange headerCells = workSheet.Cells["A1:B1"]) //this means apply the style from range A1 to B1
	    {
		    //background color light gray
		    headerCells.Style.Fill.BackgroundColor.SetColor(System.Drawing.Color.LightGray);
		    
		    headerCells.Style.Font.Bold = true; //bolden the text
			    //Refer to EPPlus documentation for more detailed styles
	    }
        
        List<Person> persons = //assume there is code here getting data from repository or DB
        
        int row = 2; //row iteration for the for loop
        //insert the data using foreach
        foreach (Person person in persons)
        {
	        workSheet.Cells[row, 1].Value = person.Id;
	        workSheet.Cells[row, 2].Value = person.Name;
	        row++;
        }
        
        //this will fit the width of all the columns when text are long
        workSheet.Cells[$"A1:B{row}"].AutoFitColumns();
			//"A1:B{row}" means: A1 is the start B is the last column since there are only two properties, 
			//{row} will be the last row iteration, so B{row} combined will be last row and last column.
        
        excelPackage.Save();
    }
    
    //bring back the cursor to the beginning since we will need to read it again from the beginning later.
    memoryStream.Position = 0; 
    return memoryStream;
}

```
###### Don't forget to adjust this code depending on the number of properties:
```c#
workSheet.Cells[$"A1:B{row}"].AutoFitColumns();
	//"A1:B{row}" means: A1 is the start B is the last column since there are only two properties, 
	//{row} will be the last row iteration, so B{row} combined will be last row and last column.
```
#### Controller
in the action method:
```c#
public IActionResult PersonsExcel()
{
	MemoryStream memoryStream = _personService.GetPersonExcelStream(); //grab the stream from the method
	
	//Then return the the excel stream as a downloadable file
	return File(memoryStream, "application/vnd.ms-excel", "persons.xlsx");
	//second parameter is the mime type of excel
	//third parameter is name of the file
	//see note FileResult for more detalye
}
```
>[!Warning]
>Since you are dealing with a database and a website, it might be necessary to **async** the methods, see: [[EF Core Async]] or [[Asynchronous Async]]. The samples above are non-async.
The samples above and below are not async. You will also async the action methods.

>[!info]
>I don't need to mention this, but just in case you forget. You execute this by adding a route attribute to the action method and a link or a button on a view that leads to the action method, that link/button will be the download button and will automatically download the file to the client.