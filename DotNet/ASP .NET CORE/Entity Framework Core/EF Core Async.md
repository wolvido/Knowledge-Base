When dealing with databases, naturally it is important use asynchronous methods to have a fast and efficient website.
Assuming you know how Async in c# works, see: [[Asynchronous Async]].

Following the .NET standard, EF Core provides asynchronous counterparts to all synchronous methods which perform I/O. These have the same effects as the sync methods, and can be used with the C# `async` and `await` keywords. For example, instead of using DbContext.SaveChanges, which will block a thread while database I/O is performed, DbContext.SaveChangesAsync can be used.
Sample:
```c#
var blog = new Blog { Url = "http://sample.com" };
context.Blogs.Add(blog);
await context.SaveChangesAsync();
```
**`context.SaveChangesAsync();`** Is what you will use most of the time usually, DONT FORGET.
>[!info]
>You will also async controller action methods.
#### Async LINQ operators
Naturally, you have to use the async versions of LINQ methods. This will be what you will async most of the time.
sample in a crud service method:
```c#
public async Task<List<Person>> GetAllPersons()
{
	return await _db.Persons.ToListAsync();
}
```
Simply create or convert the methods into async and use async methods. Lookup the rest of the async counterparts of LINQ methods in intellisense.
>[!Warning] Important
>The EF Core async extension methods are defined in the `Microsoft.EntityFrameworkCore` namespace. This namespace must be imported for the methods to be available in intellisense.

**Note** that there are no async versions of some LINQ operators such as [Where](https://learn.microsoft.com/en-us/dotnet/api/system.linq.queryable.where) or [OrderBy](https://learn.microsoft.com/en-us/dotnet/api/system.linq.queryable.orderby), because these only build up the LINQ expression tree and don't cause the query to be executed in the database. Only operators which cause query execution have async counterparts.



