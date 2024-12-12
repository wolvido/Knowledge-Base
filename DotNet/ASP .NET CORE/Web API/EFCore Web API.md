Using [[Entity Framework Core]] in Web API. 
# How-To:
- Well... it's the same thing, just refer to [[Entity Framework Core]].

-  How can you return data from EF Core queries in Web API controller actions?
	You can return data from EF Core queries in Web API controller actions by using the Ok method of the `ControllerBase`. For example, you can use return Ok(data) to return an HTTP 200 OK response along with the data retrieved from the database. see: [[Web API Request Methods]] for samples.

- Also, you can use the template "API Controller with actions, using Entity Framework" when making a simple API. It makes it easier, you only need to add the model you want to control and the DbContext. ==Not Suitable For Clean Architecture==.



