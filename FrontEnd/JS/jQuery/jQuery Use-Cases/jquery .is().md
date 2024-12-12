#jQuery 
Check whether a set of elements matches a specific selector, or if they fulfill a certain condition.
syntax:
```js
$(element).is(selector);
```
returns bolean true or false

example:
```html
<button id="myButton" class="btn primary">Click me</button>
```
```js
if ($("#myButton").is(".primary")) {
  console.log("The button has the 'primary' class.");
} else {
  console.log("The button does not have the 'primary' class.");
}
```
another sample:
```html
<div>
  <p>Click me to find out if I my parent is a div element.</p>
</div>
```
```js
if ($("p").parent().is("div")) {
  alert("Parent of p is div"); 
}
```