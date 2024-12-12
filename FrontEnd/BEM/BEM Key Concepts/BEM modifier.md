#bem 
keywords: 
	what are bem modifier
	what is a modifier bem
	bem modifier
	what exactly is a modifier

As long as it doesnt change the underlying structure, it is a modifier.  
  
In BEM (Block Element Modifier), modifiers are classes that modify the appearance, behavior, or state of a block or an element. They are used to add variation to the base style of a block or element without changing its underlying structure.  
  
A modifier class name in BEM consists of the base class name followed by two dashes "--" and a modifier name. For example, if you have a block with the class name "button", a modifier class for a disabled state might be "button--disabled".  

==Modifiers must always be on the edge of the class, so that it overrides.==
  
Here are some guidelines to help you identify modifiers in BEM:  
  
Look for variations in appearance, behavior, or state: If a class changes the way a block or element looks or behaves, it's likely a modifier. For example, a "button--small" class modifies the size of a button.  
  
Check for changes in state: Modifiers can also indicate a change in the state of a block or element. For example, a "button--active" class can be used to show that a button is currently active.  
  
Consider the context: Modifiers are specific to a block or element, so their names should reflect that. For example, a "card--featured" class would only apply to a featured card block, while a "button--primary" class would only apply to a primary button element.  
  
By following these guidelines, you should be able to identify modifiers in your BEM code and use them effectively to add variation and flexibility to your styles. 
  
#### things to remember:
a modifier must always include the original modified