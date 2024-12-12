---
keywords: |-
  
  how form sends data to backend
  file to backend
  file to controller
  File from view to backend, controller, service, etc
  front to back 
  view to controller
---
![[dasdw 1.png]] 
`form-data` is data taken from Form Fields, then routed and passed on to the Model Binding.
The Model Binding process can read the data and convert it to an object to be passed to the controller. It is the most prioritized by the model binding.
>[!Info] Not to be confused with [[FromBody]], this is f**or**m not f**ro**m.
#### How?
So Basically when you make a `<form>` tag in the html, whenever the form gets submitted it will send the form fields data to the controller action method set in the action attribute of the form eg: `<form action="/route/to/action-method-etc">`.
>[!tip]-
>its better if you use [[Form Submission and link Tag helpers]] instead of `<form action="/route/to/action-method-etc">`.

By default the data is converted into **form-urlencoded**, meaning the form will convert the form fields to query strings to be passed to the action method. Model binding would then convert the query string into objects or types for the action method.in
#### Passing File
If a form field is to pass a file (excel, img, csv, any file..) it will be binded as **form-data**, you need to set the form tag as **`<form enctype="multipart/form-data">`**, so the back knows its to be binded as a file.
see: (https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form for more details on form.
sample:
```html
<form asp-action="UploadFile" asp-controller="HomeController" method="post" enctype="multipart/form-data">
	<input type="file" id="avatar" name="name-of-file" accept="image/png, image/jpeg" />
	<button type="submit"></button>
</form>
```
Also don't forget to set `<input>` as file, and don't forget the `name="name-of-file"` attribute of the `<input>` of the file since it will be needed by the back end.
###### What if you want to insert data that has a foreign key, passing it from view to controller to service to..?
- That data that has the foreign key is the child model/table. 
- In the view simply ask the name of the parent, then pass that to the controller, the controller then uses a service method that grabs the corresponding parent using the name, once you have the parent data, grab its ID and use that as the foreign key in the child data youre trying to insert.
- in one to many relationship, you can extrapolate what to do.
- Yes, this can also work with DTO. DTO is just an intermediary.
#### From the Form Fields Model Binding, two types of data are read:
###### **form-urlencoded:**
Is used for simple small forms maybe five or six fields
###### **form-data**:
Is used for large forms and this also includes forms that accept files and such.
##### Http Request Headers and Body:
![[dasdw 2.png]]
The type of data to be passed is handled by the frontend, for net core it will be binded automatically. You only need to use specifications like [[FromQuery and FromRoute]].
#### Also See:
[[Model Binding Acceptable Data]] - to see the appropriate tool to pass data
