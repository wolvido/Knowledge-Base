Sometimes when a new element is loaded to the html, Jquery and JS won't be able to detect events on that element since it didnt check on live.
In order to check live you use:
```js
$(document).on("change",".selector", function () {
...
})
//or
$(document).on("click",".selector", function () {
...
})
```
