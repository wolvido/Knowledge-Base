#js
keywords:
	why does js find() uses function as its parameter

note: not to be mistaken with jQuery find()

because it uses that function argument as [[Knowledge Base/Programming Fundamentals/Callback]] to each item in the array.  
it runs the callback on each item, the callback takes each item in the array as its parameter, the result of the callback is the matched to the second parameter of find().
[https://linuxhint.com/array-find-function-javascript/](https://linuxhint.com/array-find-function-javascript/)  
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)