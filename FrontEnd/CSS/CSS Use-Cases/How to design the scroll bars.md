---
keywords: css scrollbar
---
[javascript - How to design overflow scroll bar specific? - Stack Overflow](https://stackoverflow.com/questions/73055069/how-to-design-overflow-scroll-bar-specific)
```css
.box1 {
  display: block;
  height: 300px;
  overflow:scroll;
}

.box2 {
  overflow: scroll;
  display: block;
  height: 300px;
}

/*Box 1 ScrollBar*/
/* width */
.box1::-webkit-scrollbar {
  width: 10px;
}

/* Track */
.box1::-webkit-scrollbar-track {
  background: #f1f1f1; 
}
 
/* Handle */
.box1::-webkit-scrollbar-thumb {
  background: red; 
}

/* Handle on hover */
.box1::-webkit-scrollbar-thumb:hover {
  background: #555; 
}

/*Box 2 ScrollBar*/
/* width */
.box2::-webkit-scrollbar {
  width: 20px;
}

/* Track */
.box2::-webkit-scrollbar-track {
  background: #f1f1f1; 
}
 
/* Handle */
.box2::-webkit-scrollbar-thumb {
  background: blue; 
}

/* Handle on hover */
.box2::-webkit-scrollbar-thumb:hover {
  background: #555; 
}
```