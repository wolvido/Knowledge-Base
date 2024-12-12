#js 
keywords:
	listen to an event
	run a script when something happens
	listen to what is happening to an element
	know what is happening to an element before it happens

syntax:
```js
element.addEventListener(event, function, options);
```
- **element**: This is the HTML element to which you want to attach the event listener.
- **event**: This is the name of the event you want to listen for (e.g., "click," "mouseover," "keydown," etc.).
- f**unction**: This is the function that will be executed when the event occurs.
- **options**: (optional): An optional object that specifies additional options for the event listener, such as whether the event should capture during the capturing phase or not.

example:
```js
const button = document.getElementById("myButton");

// Define the function to be executed when the button is clicked
function handleClick() {
  alert("Button clicked!");
}

// Attach the event listener to the button
button.addEventListener("click", handleClick);
```
Note: it is recommended to first define the function you would use in `addEventListener`  because `removeEventListener` relies on defined function to identify. Anonymous functions cannot be identified by remove listener. for more info on specifying with options see: [EventTarget: removeEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener#matching_event_listeners_for_removal)

Additional **options**:
1. **capture** (boolean, default: `false`): If set to `true`, the event listener will be activated during the capturing phase instead of the bubbling phase. Events propagate in two phases: capturing (from the root to the target) and bubbling (from the target back up to the root). By default, event listeners work during the bubbling phase.
2. **once** (boolean, default: `false`): When set to `true`, the event listener will be automatically removed after it is executed once. This is useful for scenarios where you want an event to trigger a one-time action.
3. **passive** (boolean, default: `false`): When set to `true`, it indicates that the event listener will not call `preventDefault()` on the event. This can be used to improve scrolling performance, especially for touch and wheel events.
see [addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#syntax) for more options and info.

