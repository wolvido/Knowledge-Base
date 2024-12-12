#chrome
use [web accessible resource](https://developer.chrome.com/docs/extensions/mv3/manifest/web_accessible_resources/#manifest-declaration) to declare the injected script or html:
```json
"web_accessible_resources": [
	{
	  "resources": ["injectedScript.js","injectedHTML.html"]
	}
],
```
declare the content script:
```json
"content_scripts":[
	{
		"js": ["contentScript.js"]
	}
],
```
then inject both the html and js using a content script:
```js
//this is the contentScript.JS

//inject html
fetch(chrome.runtime.getURL('/injectedHTML')).then(r => r.text()).then(html => {
    document.body.insertAdjacentHTML('beforeend', html);
    // not using innerHTML as it would break js event listeners of the page
});

//inject the script
var script = document.createElement('script');
script.src = chrome.runtime.getURL('injectedScript.js'); 
script.onload = function() {
    this.remove();
};
(document.head || document.documentElement).appendChild(s);
```
you cannot write code directly in a content script for an injected html, because it cant manipulate injected html, you need injected js to manipulate injected html.

Also works for files like:
```js
//inject audio
const audio = new Audio(chrome.runtime.getURL('audio.wav'))
audio.id = 'audio'
document.body.appendChild(audio)
```

for more info and ways to inject see: [content_scripts](https://developer.chrome.com/docs/extensions/mv3/content_scripts/)