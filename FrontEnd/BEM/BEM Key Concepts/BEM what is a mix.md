#bem 

Example:  
<div class="header">  
<div class="search-form header__search-form"></div>  
<!--  
The `search-form` block is mixed with the `search-form` element  
from the `header` block  
-->  
</div>  
```html
<div class="header">  
	<div class="search-form header__search-form"></div>  
	<!--  
	The `search-form` block is mixed with the `search-form` element  
	from the `header` block  
	-->  
</div>
```
In this example, we combined the behavior and styles of the search-form block and the search-form element from the header block. This approach allows us to set the external geometry and positioning in the header__search-form element, while the search-form block itself remains universal. As a result, we can use the block in any other environment, because it doesn't specify any padding. This is why we can call it independent. In any case the element is optional.  
###### Other uses of mixes :
 several blocks 
 ```html 
 <div class="menu head-menu"></div>
 ```  
 a block and an element of the same block 
 ``` html
 <div class="menu menu__layout"></div>
 ```  
 a block and an element of another block 
 ```html
 <div class="link menu__link"></div>
 ```  
 elements of different blocks 
 ```html
 <div class="menu__item head-menu__item"></div>
 ```  
 a block with a modifier and another block 
 ```html
 <div class="menu menu_layout_horiz head-menu">
 ```  
 several different blocks with modifiers 
 ``` html
 <div class="menu menu_layout_horiz head-toolbar head-toolbar_theme_black"><div>
 ```
###### Doesn't mixing break the [[BEM blocks]] independence?
I you let it, then yes, but you can design it so that any block can still be independent and since css can override, you can design it in a way that only selects what you need from the mix, see: [[redefinition levels]] for more info.
For example:
- lets say you downloaded a library that contains a `button` block with colors and design.
- and you want this button on your `header` block.
- so instead of fully styling a `header__button`, you can just create `header__button` without the designs, mix in `button` with it, then use `header__button` for sizing and other stuff.
- `header` will still be independent since it still has a `header__button`, just that it has no complex design.
