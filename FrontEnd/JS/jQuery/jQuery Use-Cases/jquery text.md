#jQuery 
returns all the texts of the element and the texts of its children, because dom is an object not text.
example:
```html
<div>text</div>
```
```js
$("div").text() //returns text
```
example2:
```html
<div>  
	<ul>  
		<li>text1</li>  
		<li>text2</li>  
	</ul>  
</div>
```
```js
$("div").text() //returns text1 and text 2
```