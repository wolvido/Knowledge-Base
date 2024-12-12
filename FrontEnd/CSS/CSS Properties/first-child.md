#css
```css
p:first-child {
  background-color: yellow;
}
```
- will select all p elements that are the first children of every parent. 
- If multiple parents with p children exists, it will select every p even on different parents
###### example:
```html
<p>will select this</p> 
<p>will not select this</p>

<div>
  <p>will select this</p>
  <p>will not select this</p>
</div>

<span>
  <p>will select this</p>
  <p>will not select this</p>
</span>
```

#### Combination Cases:
```css
p i:first-child {  
color: blue;  
}  
```
-first i element inside all p elements become blue  
  
```css
p:first-child i {  
color: blue;  
}  
```
-Every i element of the first p element of every division will turn blue