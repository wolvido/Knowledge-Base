#js 
keywords:
	detect if element exists without looping

```js
function waitForElement(selector) {
	return new Promise(resolve => {
		if (document.querySelector(selector)) {
			return resolve(document.querySelector(selector));
		}
		
		const observer = new MutationObserver(mutations => {  
			if (document.querySelector(selector)) {
				resolve(document.querySelector(selector));  
				observer.disconnect();  
			}
		}); 
		
		observer.observe(document.body, {  
			childList: true,  
			subtree: true  
		});  
	});  
}
```
to use function:
```js
waitForElement('.some-class').then((element) => {  
	console.log('Element is ready');  
	console.log(element.textContent);  
});
```
or use with async:
```js
const element = await waitForElm('.some-class');
```

[https://stackoverflow.com/questions/5525071/how-to-wait-until-an-element-exists](https://stackoverflow.com/questions/5525071/how-to-wait-until-an-element-exists)