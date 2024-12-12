Dynamically change the Layout Views only in a small section. Not the whole page. 
You can use it to add a js to a specific view only or use it for dynamic sections of a layout.
#### How to do it?
So for example, in the contact page, you need the footer of the layout to add a contact number.
So first, in the view page that you need to add:
```html
<h1>Contact</h1>

@section footer_section //add contact number
{
	<p>contact no:09080764532</p>
}
```
**`@section footer_section`** will be sent to the layout view.
In the layout view, you add a receiving section, so in the footer section of the layout views:
```html
<footer>
	<p>sample footer</p>
	@RenderSection("footer_section", false) //this is where the footer_section will render in the layout
</footer>
```
The second parameter of **`RenderSection`** is set to false because this render section is optional not required, because we only need this render section for the contacts page. 
#### Or you can use it to add a specific css or js to a page
in your [[Layout Views]] head add:
```html
<head>
	head codes etc...
	<link href="~/css/the-general.css" rel="stylesheet" type="text/css" />
    @RenderSection("styles", false)
</head>
```

Then in the specific page you want to apply the style to, add:
```html
@section styles {
    <link href="~/css/the-specific.css" rel="stylesheet" type="text/css" />
}
```