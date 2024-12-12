the FromBody attribute allows the model binding to accept json and xml data from the body, to the action method.
>[!Info]
>not to be confused with Form Data, this is **From**Body, not form. Form-data is binded automatically.

To use it, we enable the `[FromBody]` Attribute in the action method parameters:
```c#
public IActionResult ActionMethod([FromBody] type parameter)
{
}
```

Sample Action method:
```c#
public IActionResult Index([FromBody]Book book)
{
    return Content($"Genre:{book.Genre} Author:{book.Author} Title:{book.Title}", "text/plain");
}
```
Sample use of the action method, using raw json as input:
![[Capture 24.png]]
### XML
In case you need to accept xml instead of json, you need to add `builder.Services.AddControllers().AddXmlSerializerFormatters();` on program.cs then it works the same as the code above only difference is that it accepts xml instead of json. 
![[Capture 25.png]]