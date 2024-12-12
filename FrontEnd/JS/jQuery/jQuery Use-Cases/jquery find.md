#jQuery 
keywords:
	how jquery find works

searches through all the descendants and will get all the matched, not just one.

you can use selector expressions to specify, example:
```html
<ul>  
	<div><li>item 1</li></div>  
	<span><li>item 2</li></span>  
	<div><li><strong>item 3</strong></li></div>  
	<span><li><strong>item 4</strong></li></span>  
</ul>
```
to specify item 4:  
``$("ul").find(" span > li > strong)``

(li) would specify all  
(span) would specify item 2 and 4  
(strong) would specify item 3 and 4  
(span > strong) would throw an error  
(span > li > strong) would specify only item 4