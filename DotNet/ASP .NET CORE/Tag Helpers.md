Allows you to add asp tag helper attributes to an html markup, which essentially allows you to control the markup through the backend. Allowing you to DRY your code by using data from the back-end. 
###### Sample:
Instead of using:
```html
<input type="text" name="ModelProperty" id="ModelProperty" value="ModelValue"></input>
```
you can just do:
```html
<input asp-for="ModelProperty"></input>
```
Then assign and manipulate the attributes in the backend.
###### Other advantages:
- Dynamic links - change the link on the `<a>` tag dynamically on the backend or generate new links dynamically.
- You can bind a model in form tags such as `<form>`, `<input>`, etc., which essentially transforms your forms to fit perfectly to the model being used.
#### Import Tag Helpers
Of course first do this:
```cshtml
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```
Import in [[_ViewImports.cshtml]]
# What next?
- Specify which controller and action method the tag sends data to dynamically without specifying the url. [[Form Submission and link Tag helpers]].
- instead of doing `<input type="text" name="sample-name" id="sample-id" value="sample-value" etc..>` you can just do `<input asp-for="model" />`. Instead of manually having to add attributes to an `<input>`, `<textarea>`, `<select>`, and `<label>` tag, you can just bind it to a data type and it will automatically edit itself to accommodate input of that type. see [[Input and label tag helpers]]. 
- Easily generate the selections of the `<select>` dropdown tab, and also be able to dynamically generate it. see [[Select tag helper]].
- How to easily validate the front-end using tag helpers see: [[Client Side Validations tag helpers]]. This way you don't have to repeat validations on the backend and frontend.
- Sometimes the images in the client side does not update to the changes made by the server because the client uses cache version. If you have an image that needs to be updated soon as possible like a logo [[img tag helper]].
- In case the project uses CDN's. see: [[Script tag helpers]].