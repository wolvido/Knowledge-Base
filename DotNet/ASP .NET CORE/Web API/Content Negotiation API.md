Content Negotiation is the process of selecting the appropriate format or language of the content to be exchanged between the client and API.
Read [[Content Negotiation]] first.

So, by default the API can serve `text/plain`, `application/json`, and `text/json` mime type. 
But what if you want to serve or receive only `application/json` and not other format?
# How-To:
If you want to globally only accept and serve `application/json`, then in your `Program.cs` simply add:
```c#
builder.Services.AddControllers(options =>
{
	//add these filters
    options.Filters.Add(new ProducesAttribute("application/json"));
    options.Filters.Add(new ConsumesAttribute("application/json"));
});
```
or you can add only the produce or only the consume.
###### But what if you don't want it globally, you only need it on specific controllers or action methods?
#### `[Produces]` and `[Consumes]` Attribute
You can apply `[Produces]` or `[Consumes]` attribute on a specific controller or action method to specify what it should produce or contain.
For example, set one action method to only produce XML:
```c#
	[HttpGet]
	[Produces("application/xml")] //only produce xml for this endpoint
	public async Task<IActionResult> GetCities() 
	{
		if (_context.Cities == null)
		{
			return NotFound();
		}
		
		var cities = await _context.Cities.OrderBy(temp => temp.CityName).ToListAsync(); 
		return Ok(cities); 
	}
```
==Also, if you want to produce XML then in you need to add XML serializer:==
```c#
builder.Services.AddControllers(options =>
{
	//add these filters
    options.Filters.Add(new ProducesAttribute("application/json"));
    options.Filters.Add(new ConsumesAttribute("application/json"));
})
	.AddXmlSerializerFormatters(); //Add this if you want to produce xml
//Although, XML is very rare for api anyway since it is heavy.
```
