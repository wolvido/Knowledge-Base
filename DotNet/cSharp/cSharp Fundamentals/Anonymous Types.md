---
keywords: anonymous object
---
#cSharp 
Its an anonymous object. basically an object without behavior, just a set of data. They just hold values to be used by something else.

sample:
```c#
var student = new { Id = 1, FirstName = "James", LastName = "Bond" };
Console.WriteLine(student.Id); //output: 1
Console.WriteLine(student.FirstName); //output: James
Console.WriteLine(student.LastName); //output: Bond

student.Id = 2; //Error: cannot chage value
student.FirstName = "Steve"; //Error: cannot chage value
```
You would be able to set values if it was a real object.

you can also put another anonymous type inside an anonymous types:
```c#
var student = new 
{
	Id = 1, 
	FirstName = "James", 
	LastName = "Bond",
	Address = new { Id = 1, City = "London", Country = "UK" }
};
```

Anonymous types in C# are primarily used for short-term data storage and organization within a limited scope, such as a method or code block. They are useful when you need to group related data together, often for temporary or intermediate processing. Here are some common use cases for anonymous types:

1. Projecting Data: You can use anonymous types to project data from a collection, such as a list of objects, into a new structure that only contains the specific properties you need. This is useful for data transformation and simplifying data before further processing.
2. LINQ Queries: Anonymous types are frequently used in LINQ queries to create custom result sets or group data based on specific criteria. They allow you to define the shape of your query results on the fly.
3. Passing Data to Views: In web development with frameworks like ASP.NET MVC or ASP.NET Core, anonymous types are used to pass data to views for rendering. They provide a convenient way to package and transport data from the controller to the view.
4. Temporary Data Structures: If you need to bundle related data without defining a separate class or struct, anonymous types can serve as lightweight data structures for temporary use, such as in a specific method or operation.
5. Anonymous Objects for Configuration: Anonymous types are sometimes used to store configuration settings or parameter values for methods or components, especially when the configuration is simple and short-lived.
6. Inline Data Creation: You can use anonymous types to quickly create data for testing, mocking, or other scenarios where you need sample data without defining concrete classes.