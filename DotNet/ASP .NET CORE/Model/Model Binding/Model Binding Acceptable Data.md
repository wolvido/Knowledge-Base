---
keywords: "Http Request Data to Model Binding\ 

  send data from view to controller\ 

  \r\rsend data from frontend to backend\rsend

  \ data from front to back

  pass data from view to controller

  pass data from view to back"
---
Types of data from the frontend that is read by the Model Binding.
![[Capture 22.png]]
### Form Fields:
These are the form fields in the front end.
Sample:
![[Pasted image 20231109180528.png]]

The action attribute of the Form will be responsible for sending the data to the controller.
see: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form
So Basically when you make a `<form>` tag in the html, whenever the form gets submitted it will send the form fields data to the controller action method set in the action attribute of the form eg: `<form action="/route/to/action-method-etc">`.
>[!tip]-
>its better if you use [[Form Submission and link Tag helpers]] instead of `<form action="/route/to/action-method-etc">`.

By default the data is converted into [[form-urlencoded and form-data]], meaning the form will convert the form fields into query strings to be passed to the action method. Model binding would then convert the query string into objects or types for the action method.
If a form field is to pass a file it will be binded as **form-data**, you need to set the form tag as `<form enctype="multipart/form-data">`. see: (https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form for more details on form
### Request Body:
see [[FromBody]].
### Route Parameter Data:
Also know as [[Route Parameters]] . It is specified by the route attribute, directly set in the url.
Sample:
```c#
[Route("/bookstore/{price?}")]
public IActionResult Index(Book book)
{
	if (!ModelState.IsValid)
	{
	    return BadRequest(errors);
	}
	return Content($"book price:{book.Price}", "text/plain");
}
```
if url is `/bookstore/999` will return **`book price:999`** 
### Query String Parameter:
values set by query string. 
Sample:
URL: `/bookstore/?Author=Winzyl&Genre=Drama&Title=GameOfThrones`
```C#
[Route("/bookstore/")]
public IActionResult Index(Book book)
{
	if (!ModelState.IsValid)
	{
	    return BadRequest(errors);
	}
	return Content($"book Genre:{book.Genre} author:{book.Author} Title:{book.Title}", "text/plain");
}
```
will return **`book Genre:Drama author:Winzyl Title:GameOfThrones`**.
##### Question?
How does model binding know what input corresponds to the right property?
- either through [[Input and label tag helpers]]
- or through input name attribute.
### Request Headers:
Data from the request headers [[HTTP Request Headers]]
How to get the data?
```c#
public IActionResult Index(Person person, [FromHeader(Name = "User-Agent")] string userAgent)
{
	//codes
}
```
The data from the `"User-Agent"` key located in the request header will be stored in the **userAgent** as a string type.