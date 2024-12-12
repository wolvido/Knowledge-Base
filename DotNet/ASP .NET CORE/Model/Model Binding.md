---
keyword:
---
Model Binding is a feature that reads values from http requests and binds them in a model object. see [[Model]].
###### **What is it's purpose? What problem does it solve?**
The main purpose is to take all the incoming data from the front end and form [[Model]] objects to be manipulated by the backend controller, or in other words bind them to model objects. Model objects is what is handled by the controller. see [[Controllers]].
Why objects? because OOP.
###### **How does it work?**
![[Capture 22.png]]
The Client sends data, and the data is included in the HTTP Request, The request is then routed to the Model Binding process. Model Binding reads the Request from top to bottom, from Form fields to Query string parameters, it takes those data and converts it into objects that the Controller can use. 

The data read by Model Binding are the **`Form Fields`**, **`Request Body`**, and **`Route Data`**/**`Route Parameters`**, and **`Query String Parameter`** . for more info see [[Model Binding Acceptable Data]].

**Sample**:
lets say you have the request `/bookstore?bookId=10`, it contains query string parameter of `bookId=10`. The model binding will automatically assign 10 to any property named `bookId`.
example action method:
```c#
// url: /bookstore?bookId=10
[Route("/bookstore")]
public IActionResult Index(int bookId)
{
    return Content($"bookId:{bookId}", "text/plain"); //will return bookId:10
}
```
The Controller and the Action method already knows what the `bookId` is just by adding `int bookId` in the Action method as argument, because the built-in Model Binding process already converted the request into a `bookId` object of int type, and automatically injected it into the Action method.
In the example above we used query string parameter, as shown in the diagram above, we can also read from **`Form Fields`**, **`Request Body`**, and **`Route Data`**/**`Route Parameters`**. see [[Model Binding Acceptable Data]] for more info on the data that is acceptable.
**An Example using Route Data/Parameters**
```c#
// url: /bookstore/10
[Route("/bookstore/{bookId}")]
public IActionResult Index(int bookId)
{
    return Content($"bookId:{bookId}", "text/plain"); //will return bookId:10
}
```
will work the same as using query string a parameter.

If for example Route Data and Query String both exist as input:
```c#
// url: /bookstore/20?bookId=10
[Route("/bookstore/{bookId?}")]
public IActionResult Index(int bookId)
{
    return Content($"bookId:{bookId}", "text/plain"); //will return bookId:10
}
```
As shown in the in the image above, it follows this order: **`Form Fields`**, **`Request Body`**, **`Route Data`**/**`Route Parameters`** and **`Query String`**.
If there is route data and query string, route data will come first, unless route data is null.
So If we use url:`/bookstore/20?bookId=10` the output will be: **bookId:20**, if we use url:`/bookstore/?bookId=10` the output will be: **bookId:10**.
>[!warning]
>The sample above is to demonstrate how model binding works, in real development you use a model class as arguments to an action method. see [[Model]] on the proper way.

>[!Info] IMPORTANT NOTES and practices:
- Create a custom model binder if you need to automatically bind some data to a model or create a custom model binder. [[Custom Model Binder]].
- If you want to know where all these data come from see: [[Model Binding Acceptable Data]].
- To know more about Form Data see [[form-urlencoded and form-data]].
- How do I send data form data from view to controller? [[form-urlencoded and form-data]].
- If you need the model binding to accept Json or xml use [[FromBody]].
- If you need to know what format to accept when binding DateTime [[DateTime Model Binding]].
