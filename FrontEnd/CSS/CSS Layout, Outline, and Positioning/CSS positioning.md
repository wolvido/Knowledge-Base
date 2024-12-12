#css 
keywords:
	css position
	css types of positions
	css css fixed vs relative vs absolute vs sticky

- absolute sticks to the nearest ancestor/parent with specified positioning eg. relative or absolute. Uses the top right as base. Without an ancestor with specified positioning it uses the html as base.  
  
- relative takes the static position unless specified, when specified it uses the static position as base. Its position is relative to itself, meaning relative to the default static position.  

- Sticky positioning is a hybrid of relative and fixed positioning. The element is treated as relative positioned until it crosses a specified threshold, at which point it is treated as fixed positioned.  
  You must specify a threshold with at least one of top, right, bottom, or left for sticky positioning to behave as expected. Otherwise, it will be indistinguishable from relative positioning.
  
- fixed sticks on the viewport, uses the html as base unless specified.

https://css-tricks.com/absolute-relative-fixed-positioining-how-do-they-differ/