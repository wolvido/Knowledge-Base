[[css before after]] |
#css 
you can, but you still need to declare content, you can declare an empty content:
```css
.element::before {
  content: "";
  /* Other styles for the pseudo-element */
}

.element::after {
  content: "";
  /* Other styles for the pseudo-element */
}
```
everything starts at before or after the element but without the content.
see [[css before after]] if you dont know what that is.
