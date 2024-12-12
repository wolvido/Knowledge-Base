###### So in `Program.cs`, instead of doing this:
```c#
public class Program
{
	public static void Main(string[] args)
	{
		var builder = WebApplication.CreateBuilder(args);
		
		builder.Services.AddControllers();
		
		var app = builder.Build();
		
		app.UseHttpsRedirection();
		
		app.UseAuthorization();
		
		app.MapControllers();
		
		app.Run();
	}
}
```
###### This will be accepted instead:
```c#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```