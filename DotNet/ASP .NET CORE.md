
- MSDN recommends that all static files eg. images, javascript into web root folder named "wwwroot"

#### The annoying prerequisites
add this in program.cs:
```c#
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
```