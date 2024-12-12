To prevent the rest of the pipeline or an action method from executing and either replacing or redirecting the pipeline.
###### For Example:
- If you short circuit in the [[Authorization Filter]], it means authorization is invalid, it will prevent access to all the pipeline except for a **`IActionResult`** that informs the user that authorization is invalid.
![[Pasted image 20240308155041.png]]
---
- If you short circuit in the [[Resource Filter]], it usually means there is some error with the **resource**, it will prevent access to all the pipeline it covers, except for a **`IActionResult`** that sends an error message to the browser or a cached response. (Lookup the meaning of resource in [[Resource Filter]] note.)
![[Pasted image 20240308160134.png]]
---
- f you short circuit in the [[Action Filter]], usually it means there is some error like a validation error, it will prevent access to the action method it covers, and either redirect to another Action method or replace the result with an error message.
![[Pasted image 20240308163509.png]]
---
- The [[Exception Filter]] short circuits if there are exceptions in the processing of an http request, it will prevent the normal **`IActionResult`** from executing and usually replace it with an error message.
![[Pasted image 20240308164957.png]]
---
- For the [[Result Filter]] it will prevent the original **`IActionResult`** from executing and either replace or modify it. In the real world this is rarely used.
![[Pasted image 20240308165519.png]]
---
# How-To:
Sample:
```c#
public class PersonsListActionFilter : IActionFilter
{
	public void OnActionExecuted(ActionExecutedContext context)
	{
		//first assign the controller to a variable using is keyword, this is necessary so we can access the controller
		if (context.Controller is HomeController controller) 
		{
			if (!controller.ModelState.IsValid) //if validation is invalid
			{
				//assume there are code here...
				//var sampleArgument = ...
				
				//this code is the short circuit
				context.Result = controller.View(sampleArgument); 
					//instead of the action method returning its normal view, will be replaced by View(sampleArgument).
					//essentially, in the action method, it is equivalent to `return View(sampleArgument);`
					//the action method will not run.
				
				//OR you can redirect to another action method
				context.Result = test.RedirectToAction("Index", "Home");
					//Index is the action method name
					//Home is the controller name
					//the original action method will not run, if filter is assigned to an action method.
			}
		{ 
	}
}
```
So, if there are model validations that exist it will return a different view or redirect to another action method. Edit the code as necessary.
###### context.Result is what is used to short circuit to any result needed for any filter.
```c#
public class SampleResultFilter : IResultFilter
{
	public void OnResultExecuting(ActionExecutingContext context)
	{
		//code that will execute before the response is sent
		if(...)
		{
			return context.Result = //whatever you need to happen to the result
			
			//sample:
			return context.Result = new NotFoundResult(); //404 not found
		}
	}
}
```
#### Of Course this is not limited to Action Filters only