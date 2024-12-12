Interface type that is used as the return of an action method.
	**What is an action method?**
	A  method of a controller class that has a Route Attribute. It is the direct action connected to the route URL attribute. Action methods return action results, these action results are what is needed by the client, samples of action results are [[Content Result]], [[JsonResult]], etc.. All action results are derived from `IActionResult`. 

All of its children is used as a return of an action method. It's children are:
[[Content Result]], [[FileResult]], [[JsonResult]], [[Redirect Results]], [[Status Code Results or Error Results]].
	Usually used for API: [[CreatedAtActionResult()]], [[NotFound()]], [[NoContent()]], [[Problem()]].

**Why is `IActionResult` the return type of all action methods?**
For versatility, because action methods need to return **content**-`ContentResult`, **JSON**-`JsonResult`, **Files**-`FileResult`, etc.. for the client to handle. A JSON, or a File, or anything has an equivalent action result type such as `JsonResult`,  because we are using an OOP language, it has an equivalent object to be manipulated.
All these action result types have one parent, and that is `IActionResult`. So if you have an action method that may return a content or a json and you assign it a return type of `ContentResult`, it will throw an error for a `JsonResult` return. If you use `IActionResult` as  the return type, it can return a `ContentResult` and a `JsonResult`, since all action results are the children of `IActionResult`.
#### **Important Notes:**
- if you want to throw errors use: [[Status Code Results or Error Results]]
- if you want to redirect use: [[Redirect Results]]


![[ac.png]]