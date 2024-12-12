#js #jQuery 
keywords:
	track mouse movement
	move element to mouse
	move to where mouse is
	mouse movement

`event.pageY`
`event.pageX`

example:
```js
document.addEventListener("mousemove", function(event) {
  const xPosition = event.pageX;
  const yPosition = event.pageY;
  console.log(`Mouse X-coordinate: ${xPosition}px, Y-coordinate: ${yPosition}px`);
});
```

you could use it to move an element on your mouse like: 
```js
$('*').click(function(event) {
	$("element").css({
		top: event.pageY,
		left: event.pageX
	});
});
//can be used for a right click context menu
```

another example:
[event.pageY | jQuery API Documentation](https://api.jquery.com/event.pagey/)