#html 
#### Inline:
- vertical division  
- will take space on the next vertical space, has no height  
###### example:
line 1: X X X
___
#### Block:
- horizontal division  
- will take space horizontally  
###### example:
line 1: X  
line 2: X  
line 3: X  
 ___ 
###### There is also Inline-block, its like inline but you can height

![[Capture 52.png]]


see: [[span vs div]] for more info.

>[!note]
>You cannot put block elements in an inline element. An inline by definition does not extend below. If your "inline" extends below then it is not inline, it is a block and you should use a block or another block element. 
>This means, you cannot put a block inside a span.