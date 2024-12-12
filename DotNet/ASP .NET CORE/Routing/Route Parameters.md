>[!info]
>This uses endpoints, this is not what you would usually use in real world dev, see route parameters in [[Model Binding Acceptable Data]] instead.

basically parameters in the link
sample:
```c#
app.UseEndpoints(endpoints =>
{
    endpoints.Map("files/{filename}.{extension}", async context =>
    {
        string? filename = Convert.ToString(context.Request.RouteValues["filename"]);
        string? extension = Convert.ToString(context.Request.RouteValues["extension"]);
        
        await context.Response.WriteAsync($"File - {filename} - {extension}");
    });
});
```
you can put whatever in the link, for example:
if the link is `url/files/file.txt` will output: File - file - txt
#### You can also set a a default route parameter
sample:
```c#
endpoints.Map("products/{id=1}", async context => //just add =
{
    int id = Convert.ToInt32(context.Request.RouteValues["id"]);
 
    await context.Response.WriteAsync($"Product ID: {id}");
});
```
if the link is `url/products/` or `url/products` will output: Product ID: 1

![[Capture 16.png]]
#### You can also set an optional values:
![[Capture 17.png]]
It works just like default route parameter but will return null if no parameter is provided.
it's best used if you have a value that you allow to be null. Because some values can also be optional.
Can also be used to just check if value is null and force user to input a value.
sample:
```c#
endpoints.Map("products/{id?}", async context =>
{
    if (context.Request.RouteValues["id"] == null)
    {
        await context.Response.WriteAsync($"ID is empty");
    }
    else
    {
        int id = Convert.ToInt32(context.Request.RouteValues["id"]);
        await context.Response.WriteAsync($"Product ID: {id}");
    }
});
```
You can also restrict what values can be accepted, see [[Route Constraints]]

**NOTE:** The samples given above should not be used in real life, use controllers and view models. [[Controllers]], [[Model Binding]]



