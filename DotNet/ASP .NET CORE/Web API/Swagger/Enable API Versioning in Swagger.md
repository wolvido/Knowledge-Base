Assuming you've implemented [[API Versioning]], you now need to enable it in Swagger.
# How-To:
###### 1. Swagger documentation will need to be enabled for every API version.
In `Program.cs`:
```c#
builder.Services.AddSwaggerGen(options =>
{
	options.IncludeXmlComments(Path.Combine(AppContext.BaseDirectory, "api.xml"));
	
	options.SwaggerDoc("v1", new OpenApiInfo
	{
		Title = "Name/Title of the API",
		Version = "v1"
	});
	 
	options.SwaggerDoc("v2", new OpenApiInfo
	{
		Title = "Name/Title of the API",
		Version = "v2"
	});
	
	//add v3 if you want...
});
```
You enable one for every version.
###### 2. Create Endpoints in Swagger UI
In `Program.cs`:
```c#
var app = builder.Build();
app.UseSwagger();
app.UseSwaggerUI(options =>
{
    options.SwaggerEndpoint("/swagger/v1/swagger.json", "Name-of-API v1");
    options.SwaggerEndpoint("/swagger/v2/swagger.json", "Name-of-API v2");   
});
```
###### 3. Explorer
Currently Swagger can't read versions in the URL, so we set it up in `AddApiExplorer()`.
In `Program.cs` alongside `AddApiVersioning` and `AddMvc`:
```c#
builder.Services.AddApiVersioning(config =>
{
	//codes...
	//read note API Versioning if you forgot this.
})
    .AddMvc()
    .AddApiExplorer(options => //ADD THIS
    {
        options.GroupNameFormat = "'v'VVV";
        options.SubstituteApiVersionInUrl = true;
    });
```
small 'v' is the pre-fix in the url, while `VVV` means the version accepts three digits, example it will accept `v1.00`.
