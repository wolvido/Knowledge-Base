#css
The CSS overflow property controls what happens to content that is too big to fit into an area. basically it handles what happens when content overflows. 

Like when the text your typing reaches the border, does it create a scrollbar or does it continue and just hide itself?

1. `visible` (default): This value allows the content to overflow the element, potentially overlapping other elements. This is the default behavior.
```css
overflow: visible;
```

2. `hidden`: This value hides any content that overflows the element. It effectively clips the content, making it invisible if it doesn't fit within the boundaries of the element.
```css
overflow: hidden;
```

3. `scroll`: This value adds scrollbars (both vertical and horizontal, if needed) to the element, allowing users to scroll and view the content that overflows.
```css
overflow: scroll;
```

4. `auto`: Similar to `scroll`, this value adds scrollbars only when necessary. If the content fits within the element, no scrollbars are displayed.
```css
overflow: auto;
```

See: [[How to design the scroll bars]].