#bem 
keywords:
	# mix or modifier

Let's assume that links in your project are implemented via a link block. We need to format menu items as links. There are several ways to do that. 
-Create a modifier for a menu item that turns the item into a link. Implementing such a modifier would necessarily involve copying the behavior and styles of the link block. That would result in code duplication.  
OR 
-Have a mix combining a generic link block and a link element of a menu block. A mix of the two BEM entities will allow us to use the basic link functionality of the link block and additional CSS rules of the menu block without copying the code.

should I use a mix or modifier, in the context of an already existing implementation?  
-use a modifier if you plan to reuse the implementation and its modifier.

-use a mix if the mixed implementation will not be reused.  
OR  
-If it sets the external positioning.