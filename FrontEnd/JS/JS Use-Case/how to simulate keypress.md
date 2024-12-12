---
keywords: simulate real keypress
---
[[how to monitor keypress events]] |
#js
when a key is pressed an event is dispatched, you need to find the event and use dispatchEvent() to dispatch the event. To find out what event occurs see [[how to monitor keypress events]].
  
To simulate press enter:  
```js
let element = getElementBy#("element#"); //the targeted element to press enter (required)

element[0].dispatchEvent(new KeyboardEvent('keydown', {bubbles:true, key:'Enter', code:"Enter", charCode:0, keyCode:13, which:13 }));  

element[0].dispatchEvent(new KeyboardEvent('keypress', {bubbles:true, key:'Enter', code:"Enter", charCode:13, keyCode:13, which:13 }));  

element[0].dispatchEvent(new KeyboardEvent('keyup', {bubbles:true, key:'Enter', code:"Enter", charCode:0, keyCode:13, which:13 }));  
```
  
Works on any other keys, just change the key code and charcode.  
Keydown, press, and up is included to be sure.

To 
