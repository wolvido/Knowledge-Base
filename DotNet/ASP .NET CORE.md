
- MSDN recommends that all static files eg. images, javascript into web root folder named "wwwroot"

#### Exception page enable for dev env
add this in program.cs:
```c#
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
```