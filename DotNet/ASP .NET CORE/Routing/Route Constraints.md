Adding constraints for route parameters see [[Route Parameters]].
This is used to limit the route parameter inputs. They are not a substitute for comprehensive data validation and user input validation. It makes no sense to prevent wrong inputs, when the user doesn't even know that its a wrong input.

sample:
```c#
endpoints.Map("products/{id:int}", async context => //if id is not int, endpoint will not execute
{
    int id = Convert.ToInt32(context.Request.RouteValues["id"]);
    await context.Response.WriteAsync($"Product ID: {id}");
});
```
##### All allowed constraints:
**int:** This constraint ensures that the parameter is a valid integer.
```c#
[Route("api/{id:int}")]
```
**bool:** Ensures that the parameter is a valid Boolean value (`true` or `false`).
```c#
[Route("api/{isActive:bool}")]
```
**alpha:** Restricts the parameter to contain only alphabetic characters.
```c#
[Route("api/{name:alpha}")]
```
**regex:** You can use a regular expression to define custom constraints.
```c#
[Route("api/{code:regex(^\\d{5}$)}")]
```
**min/max:** You can set minimum and maximum values for numeric parameters.
```c#
[Route("api/{age:min(18):max(99)}")]
```
**range:** Specifies a range of values for numeric parameters.
```c#
[Route("api/{score:range(0, 100)}")]
```
**length:** You can specify the minimum and maximum length for a string parameter.
```c#
[Route("api/{username:length(3, 20)}")]
```
**enum:** Ensures that the parameter is a valid value from an enum.
```c#
[Route("api/{status:enum(MyApp.Status)}")]
```
**required:** This constraint ensures that the parameter is present in the route.
```c#
[Route("api/{id:required}")]
```
**custom constraint:** You can create custom constraints by implementing the `IRouteConstraint` interface and registering them in the application.
```c#
[Route("api/{value:customConstraint}")]
```
 For more info in custom route constraints, see: [[Custom Route Constraints]]
