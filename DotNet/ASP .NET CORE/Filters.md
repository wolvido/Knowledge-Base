Filters are methods that execute before and after the action method executes.
As soon as the router middleware picks up an action method, then it executes the filter pipeline.
![[Pasted image 20240229161049.png]]
**Their goal is to prepare the request and response from the client to server.** 
The chart shows the filter pipeline or also called the processing pipeline.
This chart assumes you know what [[Model Binding]] is and what [[Middleware]]s are.
#### What's the point?
###### **Encapsulation aka Reusability and Extensibility:**
- Filters allow you to decouple and encapsulate cross-cutting concerns (like authorization, logging, validation) into reusable components.
	- So for example, instead of creating user authorization on the action method, you can simply create a authorization filter class that is decoupled from the controller and "inject" it in the controller. (filters are not really injected, its attributed).
- This promotes cleaner and more maintainable code by **avoiding duplication** of logic across multiple controllers.
###### **Separation of Concerns:**
- Filters enable a clear separation of concerns by allowing you to organize different aspects of request processing (e.g., authentication, logging) into distinct filter classes.
##### Essentially instead of adding validation, logging, authorization in the controller, you can separate it to another layer.
Assuming you know why separation is good.
The different filters have different purposes, each will be explored in this section.
>[!info]
>By default, the broader scoped filters will always run sooner than the narrower scoped. see: [[Custom Order of Filter Execution]]
# Example: How-To create an Action Filter class
- First in you main project, create the folder "Filters". This folder will contain all types of filters.
	- **NOTE**: If using [[Clean Architecture]], "Filters" will be created in the [[UI Layer]].
- Then, create a sub folder called "ActionFilters".
	- Of course if you're creating other types of filters like Result Filter, name it "ResultFilter".
- Create a new item on the folder, name it appropriately depending on its purpose, for example if your Index Action method returns a list of **`Person`** type, and you need to filter the list, name it **`PersonsListActionFilter`**.  Name it by its purpose.
- Then inherit from **`IActionFilter`**. **`IActionFilter`** has the two method contracts **`OnActionExecuted`** and **`OnActionExecuting`**, implement it on your Action Filter.

Syntax:
```c#
public class PersonsListActionFilter : IActionFilter
{
	public void OnActionExecuting(ActionExecutingContext context)
	{
		//code that will execute before the action method
	}
	public void OnActionExecuted(ActionExecutedContext context)
	{
		//code that will execute after the action method
	}
}
```
##### **`ActionExecutingContext`** is the context of the executing action method.
Essentially, here you can access the action arguments, http context, controller, route data, all the properties you need to access for the action method executing.
This is also where you can access the view bag/view data, through accessing the controller. You'll see everything in intellisense.
This is what you will use to set up data for whatever logic you need.
#### Applying the filter
To attach the action filter to the action method:
```c#
[TypeFilter(typeof(PersonsListActionFilter))]
public async Task<IActionResult> Index()
{
	//codes...
}
```
If you need to asynchronize, see [[Asynchronous Filter]].
#### The Filters:
- [[Action Filter]] - filter for the action methods.
	- Learn to add parameters/arguments to filters; [[Filter with arguments]].
- [[Class Level Filter]] - filter for all the action methods of the controller class.
- [[Global Level Filters]] - filter for the entire project.
- [[Result Filter]] - Exactly the same as Action Filter but instead of filtering the action method, it filters the view/IActionResult to be returned by the action method.
- [[Resource Filter]] - Filters the result of the whole pipeline. aka the resource.
- [[Authorization Filter]] - As the name suggest it handles authorization. Checks if the user is authenticate or not before proceeding.
- [[Exception Filter]] - Catches exceptions in the processing of an HTTP request.
- [[IAlwaysRunResultFilter]] - Result Filter the will always run regardless of short circuit or anything.
- [[Endpoint Filters]] - Everything mentioned above are filters for controllers, [[Endpoint Filters]] is used to filter [[Endpoint]]s, the one you use in [[Middleware]]. This is mostly used in [[Minimal API]].
#### What next?
- [[Inject to a Filter]] - How to inject anything the the filter might need like services.
-  [[Custom Order of Filter Execution]] - The default execution order of the filters is that the broader scoped filters will always run sooner than the narrower scoped. You can customize the Filter order of execution.
- [[Asynchronous Filter]] - in case you need the filters to use some asynchronous methods.
- [[Filter Short Circuit]] - if you need the filter to prevent the action method from executing; in case of some validation errors.
- [[Filter Overrides]] - Override execution of a specific filter. Preventing the execution of a filter to a specific action method.
- [[Service Filter]] - don't get confused, Its not a filter for services. It is exactly the same as **`TypeFilter`** but without arguments.
- [[Filter Attribute]] - Apply Filters as a direct attribute instead of through **`TypeFilter`**.
- [[IFilterFactory]] - suppose to be factory pattern, but not really, read it, might be useful still. 
#### Interview Questions
- [[Filter vs Middleware]]

