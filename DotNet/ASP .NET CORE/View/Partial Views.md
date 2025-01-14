>[!warning]
>View Components and partial views cannot use `@section` and implement its own unique js script and css style.
>
>If you really need to theres a workaround, but if you are using jquery and other libraries, it will be loaded twice. workaround: https://github.com/aspnet/Mvc/issues/2910#issuecomment-356276338
>
>The workaround is to essentially create a special `_Layout` for partial views that has its own [[Section Layout Views]], then apply the layout to the partial views.
###### Partial Views are views that cannot be invoked individually by a controller. It is invoked by other views to be part of the bigger view. 
Can be used as a reusable BEM block to be invoked anywhere or if you need anything to be reusable, like a razor function on many views. Very useful for DRY. 
For Example, you made a table or a navigation partial view and you want to reuse that view into many normal views.
>[!warning]
>DO NOT use partial views if you have complex rendering logic or code execution is required to render the markup. Use [[View Components]] instead.
>DO NOT pass data from parent view to partial view, partial views are designed to be independent.
>###### Use Partial views when:
> - If you want to split your larger mark up files
> - You want to reduce redundant file across your project.
> - minimal straightforward CRUD server side logic that will not require significant business logic.
>
>Only use partial view to serve UI/html with data, It should not have complex rendering or business logic, also you should not use a controller to give PartialView some complex rendering logic. That is not the purpose of a controller.
## So How do I set up a partial view?
#### First the Folder Structure:
It should be in the shared folder since it will be used by everyone.
#### Naming:
Because it is shareable, its name should be prefixed with "`_`", then add the word **Partial** as postfix.
sample: `_SamplePartial.cshtml`. It is not strictly needed to be PascalCase, some use camelCase, but mosh and Harsha use Pascal.
>[!note]-
>All views that are not served directly must be prefixed with an underscore "`_`".
>Except for View Components because view components are named default.
#### Invoke the Partial View from a Normal View:
First you create the Partial View, create it just like any other view, but it needs to be self-contained and can be positioned in other views like a BEM block.
For example you created the **`_SamplePartialView`**.

Then add the tag helpers in your [[_ViewImports.cshtml]]:
```cshtml
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

Then in order to invoke the partial view, in its Parent View, you add the `<partial>` tag, and add the name of the partial view.
```html
<partial name="~/Views/Shared/_Header.cshtml"></partial>
```
You can also add a css class to the partial like:
```html
<partial class="sample-class" name="_SamplePartialView"></partial>
```
For strongly typed partial view:
```html
<partial name="~/Views/Shared/_Header.cshtml" for="Model"></partial>
```
#### Other Methods:
There are also other methods that work the same as `<partial>` tag:
- `@await Html.PartialAsync("_SamplePartialView")` - Works the same as partial tag.
and also:
- `@{ await Html.RenderPartialAsync("_SamplePartialView"); }` - works the same but streams the partial view instead. It offers faster performance if there is large amount of content in the partial view.
---
# What do I need to know after this:
- Can I use ViewData/ViewBag with on partial view? **Yes**, any ViewData accessed in the parent view will automatically be copied and the copy will be set to the rendered partial view. So it acts as if the contents of a partial view is the content of the parent view. 
- How to bind a model to a partial view and create a strongly typed partial view just like a [[Strongly Typed Views]]? answer: [[Strongly Typed PartialView]].
- What if you want to load the partial view dynamically with data from the backend? What if only after a press of a button you want to load the strongly typed Partial View in the parent view? You return a [[PartialViewResult]].
