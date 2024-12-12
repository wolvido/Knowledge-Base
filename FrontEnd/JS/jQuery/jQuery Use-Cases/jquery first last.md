#jQuery 
returns the first match found or the last
keywords:
	jquery how to get the first sibling
	jquery how to get first item in a list
	jquery how to get the last sibling
	jquery how to get last item in a list
example:
```html
<ul>
	<li>list item 1</li>
	<li>list item 2</li>
	<li>list item 3</li>
	<li>list item 4</li>
	<li>list item 5</li>
</ul>
```
```js
$( "li" ).first().css( "background-color", "red" ); //returns a red background on item 1
```

