#js 
keywords:
	what is e in js

The **e** stands for an event. You are capturing the event. It automatically captures the event without defining the event. It is only applicable in event handlers/listeners.
###### question:
If it automatically captures the event why do we need to write function(e), why not just function()?
- How are we suppose to refer to the object without e? you can use any letter, e is standard.

Note: `e` is not to be confused with `this` , or `event.target`.  `e` captures the event that happened not the element.