#jQuery 
keywords:
	# cycle through active in a menu of buttons

```js
$(".menu-class > li > button").click(function() {
	$('.menu-class > li > button.active').removeClass('active'); 
	$(this).addClass("active");
});
```
will remove all active in a menu of buttons