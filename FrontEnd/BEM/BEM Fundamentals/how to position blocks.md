#bem 
keywords:
	# BEM External geometry and positioning  
	# BEM positioning
	BEM how to position

The parent block should not have positioning code, positioning code can only be put in the element. To position a block relative to other blocks mix it using a block higher up in the node, if there isn't one create one. its ok to create one in the highest node which is the body and name it the page block, and use the page block elements to position the blocks in the lower node, ex:  
[https://en.bem.info/methodology/html/#positioning-a-block-relative-to-other-blocks](https://en.bem.info/methodology/html/#positioning-a-block-relative-to-other-blocks). create elements in the higher node to mix with the block, then put positioning code in the higher block.  
  
styles that are responsible for the external geometry and positioning are set via the parent block.  
[https://en.bem.info/methodology/css/#external-geometry-and-positioning](https://en.bem.info/methodology/css/#external-geometry-and-positioning)