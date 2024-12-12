#js 
keywords:
	js ?
	js question mark

shortcut for if else  
good use for toggles and switching variable values  
example:
```js
$("aside").click(function(){  
	let position = $(this)[0].style.right == "0px" ? "-465px" : "0px";  
	$(this).css("right",position);  
});
```
or
```js
$(document).ready(function() {  
	$('#toggle-button').click(function() {  
		var toggleWidth = $("#toggle").width() == 300 ? "200px" : "300px";  
		$('#toggle').animate({ width: toggleWidth });  
	});  
});
```
