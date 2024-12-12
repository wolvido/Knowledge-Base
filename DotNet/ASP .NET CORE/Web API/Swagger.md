Swagger is a set of open-source tools that help developers to generate interactive UI to document and test [[RESTful]] services.
Swagger is built on top of Open API. Open API is a specification for building and documenting APIs. It defines a standard, language-agnostic interface to describe the functionality of RESTful APIs. It is not an API or a framework.
There's also another tool called Swashbuckle, it is a framework that makes it easy to use swagger.
![[Pasted image 20240508082928.png]]
**These three are usually used together.**
#### So what's the point of this? 
it's a tool for testing and documenting API's, just like using postman but it's integrated and with documentation tools. Makes testing easier and documenting easier.
# How-To:
- **First**, nuget install `Microsoft.AspNetCore.OpenApi`.
- Also, `Swashbuckle.AspNetCore`. Swashbuckle automatically installs swagger.
#### Adding Swagger Service
add this in your `Program.cs`:
```c#
//Swagger
builder.Services.AddEndpointsApiExplorer(); 
	//enables swagger to read Metadata of every endpoint/action method
builder.Services.AddSwaggerGen(); 
	//configures swagger to generate documentation for the endpoints
```
Then after you have called `builder.Build` enable swagger and swagger UI:
```c#
var app = builder.Build();

app.UseSwagger(); //creates endpoint for swagger.json

app.UseSwaggerUI(); //creates swagger UI for testing all edpoints
```
Now navigate to "/swagger/index.html" there you will find the swagger UI tool.
![[screenshot-1715130287070.png]]
It's more convenient as it shows the options and you can test it with the swagger UI.
# What next?
- [[Documentation Comments - Swagger]] - Aside from a testing tool, Swagger is a documentation tool. API needs to be documented of course.
- [[Enable API Versioning in Swagger]] - explains itself.