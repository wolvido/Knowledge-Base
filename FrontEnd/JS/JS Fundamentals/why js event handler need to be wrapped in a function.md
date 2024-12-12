#js 
keywords:
	why js uses anonymous as an event handler argument
	why an event handler needs to be inside an anonymous function

example:  
```js
$( "#target" ).click(function() {  
alert( "Handler for .click() called." );  
}); 
``` 
why not use this:  
```js
$( "#target" ).click(alert("You clicked it."));
```
Because by not wrapping it as a function, you are calling it immediately instead of being passed as an event handler.  
  
alert( "Handler for .click() called." ) returns: undefined, that makes no sense since undefined can't be an event handler.  
  
function() {alert( "Handler for .click() called." );} returns: alert( "Handler for .click() called." );, which will work as an event handler.  
  
By wrapping an expression as a function, the function alert( "Handler for .click() called." ); will be passed on to .click() as an event handler. If you dont wrap it, the function will run and return undefined, then undefined will be passed on to .click() as an event handler, which makes no sense and will throw an error.  
  
You need the function not the output of that function.  
  
[https://stackoverflow.com/questions/19612893/jquery-why-use-anonymous-functions-as-argument](https://stackoverflow.com/questions/19612893/jquery-why-use-anonymous-functions-as-argument)