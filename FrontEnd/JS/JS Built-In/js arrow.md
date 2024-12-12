#js 
keywords:
	js method syntactic sugar

```js
var sample = a.map(function(s){ return s.length });

var sampleWithArrow = a.map(s => s.length);

s => s.length
//s is the variable, at the end of the arrow is the return, the arrow is basically pointing to the return.
```
# Important Note:
the arrow function does not have its own scope, unlike a traditional anon function, thus when using keyword `this`, this will refer to the outside scope on the arrow function.

