#css 
keywords:
	css gradient parameters
	css gradient syntax 
	css gradient formal syntax

radial syntax:
```css
radial-gradient( <ending-shape> or <size> at <position> , <color-stop-list> )
```
size - closest-side, closest-corner etc... if empty defaults to ellipse.  
ending shape - circle or ellipse. if empty defaults to ellipse.  
position - top, bottom, or 100%, if empty defaults to center.  
color stop list - colors to transition to. example: ``#ff9900 0%, #ff6600 50%, #ff0000 100%``

general example:
```css
.gradient-example {
  width: 200px;
  height: 200px;
  background: radial-gradient(circle, #ff9900 0%, #ff6600 50%, #ff0000 100%);
}
```

see [[css gradient effects]] for usage.