Sends a file as an action result

Before you can return files, you have to enable static files:
```c#
app.UseStaticFiles();
```
## There are 3 types of file results:
#### VirtualFileResult 
- Represents a file within WebRoot or wwwroot folder by default.
```c#
return File("file relative path", "content type");
```
sample:
```c#
public class SampleController : Controller
{
	[Route("/helloVirtualFile")]
	public IActionResult FileDownloadVirtual()
	{
		return File("/sample.pdf", "application/pdf");
	}
}
```
#### PhysicalFileResult 
- file that is not part of the project folder, outside the project folder, outside the wwwroot.
```c#
return PhysicalFile("file absolute path", "content type");
```
sample:
```c#
public class SampleController : Controller
{
	[Route("/helloPhysicalFile")]
	public IActionResult FileDownloadPhysical()
	{
		return PhysicalFile(@"c:\repo\project\sample.pdf", "application/pdf");
	}
}
```
#### FileContentResult 
- Represents a file from byte []. This is useful for advanced specific use cases such as encryption or returning only a part of the file.
```c#
return File(byte_array, "content type");
```
sample:
```c#
public class SampleController : Controller
{
	[Route("/helloFileContent")]
	public IActionResult FileDownloadContent()
	{
		byte[] bytes = System.IO.File.ReadAllBytes(@"c:\project\sample.pdf")
		return File(bytes, "application/pdf");
	}
}
```
If youre confused about why methods like `file()` and `PhysicalFile()` are being returned, they are just built in shortcut from `ControllerBase` it returns the same thing as the longer version, see [[Content Result]] for how it works.


