#css 
keywords:
	how to make pseudo element fill the parent

```css
.class {
	position: relative;  
}
.class:before {
	position: absolute;  
	width: 100%;  
	height: 100%;  
	content:"";  
}
```