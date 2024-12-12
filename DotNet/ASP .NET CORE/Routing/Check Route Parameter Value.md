---
keywords: how to get the value of a route parameter
---
```c#
[Route("/file{id:int}")]
public IActionResult FileHandling()
{
    int? id = Convert.ToInt32(Request.RouteValues["id"]);
}
```
This is using Request.RouteValues of Http Context Directly. <mark style="background: #FF5582A6;">This is/was for educational only.</mark> 
See [[Model Binding]] to see how the value of a route parameter is really taken.

See [[What is HttpContext or context]] for more detalye.