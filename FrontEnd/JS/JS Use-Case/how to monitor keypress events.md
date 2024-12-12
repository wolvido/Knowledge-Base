[[how to simulate keypress]] | 
#js 
keywords:
	js javascript how to get keypress code
	js javascript how to get keypress event
	js javascript how to monitor keypress event
```js
document.addEventListener('keydown', (event) => {  
	console.log(event)  
});
document.addEventListener('keypress', (event) => {  
	console.log(event)  
});
document.addEventListener('keyup', (event) => {  
	console.log(event)  
});
```
once you know the event, you can use dispatch event. See [[how to simulate keypress]].