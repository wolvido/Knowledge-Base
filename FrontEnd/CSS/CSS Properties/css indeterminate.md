#css 
keywords:
	css not check not unchecked
	css checked third state

The :indeterminate selector selects form elements that are in an indeterminate state.  

Indeterminate refers to the state of certain HTML elements, like checkboxes and radio buttons, where it's not clear whether they are selected or not. These elements have three states: checked, unchecked, and indeterminate.
  
The :indeterminate selector can only be used on:
```html
<input type="checkbox">
<input type="radio">
<progress> 
```

sample:
```css
/* Selects any <input> whose state is indeterminate */
input:indeterminate {
  background: lime;
}
```
  
it needs JS to set an element into indeterminate.  
  
[https://developer.mozilla.org/en-US/docs/Web/CSS/:indeterminate](https://developer.mozilla.org/en-US/docs/Web/CSS/:indeterminate)  
[https://www.w3schools.com/cssref/tryit.php?filename=trycss3_sel_indeterminate](https://www.w3schools.com/cssref/tryit.php?filename=trycss3_sel_indeterminate)