#js 
keywords:
	js identify where the event occured
### event.currentTarget
refers to the dom where the **event listener is attached to**, it identifies the event that happened in the element where the event listener is attached to. Basically when an event propagates, if it affected the element where the event listener is attached, it will return that element not the one where the event came from.
kind of like `this` in a regular function.
Note: it is only similar to `this` when using regular function not arrow function. see [[JS scope]] for more details.

### event.target
refers to the dom where the **event occurred** even if the event handler is attached to a parent or a grandparent, it will return the element where the event originated. It knows through propagation.


