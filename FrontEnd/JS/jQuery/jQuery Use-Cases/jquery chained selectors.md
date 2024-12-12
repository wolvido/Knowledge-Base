#jQuery 
keywords:
	jquery with two parameters
	jquery with multiple selectors
	jquery with multiple parameters
	jquery with two selectors
	jquery with comma in middle of selectors
	comma separated selector in jquery
	space separated selector
	jquery selector space in the middle
#### comma separated chain syntax:
```js
$(“selector1, selector2, selectorN”);
```
is equivalent to:
```js
$(“selector1”);
$(“selector2“);
$(“selectorN“);
```

There is also another one where the comma is outside the " ".
#### syntax:
```js
$(expr, context);
```
is equivalent to:
```js
$(context).find(expr)
```

#### space separated chain syntax:
```js
$("selector1 selector2 selector3 selectorN");
```
searches for all children of selector1 that is a selector2, and then searches for all children of selector2 that is a selector3, so on and so forth.
