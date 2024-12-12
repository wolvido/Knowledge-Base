What I learned so far:
An angular component is a like a BEM block with behaviors and an HTML.
- So basically a more defined, more compact, more class like Block.
- Like a block with its own HTML, CSS, JS, instead of just JS and CSS.
- A block that can have children block. Solves the problem of the confusion on whether this element should be a mixed outside block or part of the block, of if an element should be a block. 
- Solves the confusion on whether A block is just a skeleton, or does it bring its own style.
- BEM block made OOP.
To be more exact, a standalone parent component is a block, also called a feature. While the child components are the elements of those blocks, they can also import other shared components. which are the small UI components.

The standalone parent component/Feature will be the largest self contained Block. An example of this is the calendar block of BEM.


