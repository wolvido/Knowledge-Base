It is rare, but in case you need an html tag that enables or disables depending on the environment.
# How?
#### Import Tag Helpers
First import tag helpers in [[_ViewImports.cshtml]].
```cshtml
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```
#### Exclude Include
If you need an element only to appear in development environment:
```html
<environment include="Development"> //you can change this to whatever emvironment
	//whatever is needed
	<h1>This is the Development page </h1>
	<button> Button only for development </button>
</environment>
```
What if you need the element to appear anywhere **except** in development environment:
```html
<environment include="Development">
	<h1>This is not a Development page </h1>
	<button> Button for non development page </button>
</environment>
```
