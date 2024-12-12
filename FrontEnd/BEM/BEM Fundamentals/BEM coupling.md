[[When to DRY]] | [[BEM what is a mix]]
#bem 

do not use coupled CSS like this:
```css
.class1, .class2 {  
	font-family: Arial, sans-serif;  
	font-size: 14px;  
	color: #000;  
}
```
in general, coincidental similar code should still be separate, and should not be forced DRY, refer to [[When to DRY]] for reference.

But if it is self contained, it can be made into a block. You can mix it instead: ([[BEM what is a mix]])  
```css
.bem-block {  
	font-family: Arial, sans-serif;  
	font-size: 14px;  
	color: #000;  
}
```