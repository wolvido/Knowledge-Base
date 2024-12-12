#css 
The ability to set a default height but it reduces when squeezed.
- Not media query, the flex like style.
- It only squeezes the empty spaces.
# How-To:
- there is actually no such thing, the closest thing we can do is to reduce the parent based on it percentage.
```css
target{
	height: 115px; //default-height
}

parent{
	height: calc(100% - 64.5px);
	display: flex;
	flex-direction: column;
}
```
Assuming there is empty space inside the target, the space will reduce below `115px`.