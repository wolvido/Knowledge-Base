#html
The DOM is a changeable model of the HTML elements. You see, a web page could be directly rendered like this: HTML string -> pixels. However, this would make it hard to introduce dynamic behavior. (Lots of string search/replace in the HTML string.) So instead, the browser first parses the HTML into an object: HTML -> DOM. When the DOM changes, then the browser re-renders it. DOM -> pixels. The DOM can be changed by user interaction (for example, typing in a text input automatically updates the value attribute) or Javascript.  
  
So it is basically what js is modifying rather than directly changing the HTML string.  
