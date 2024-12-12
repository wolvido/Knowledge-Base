#html 
they are both generic and used the same way except: 
- div are for block elements  
- span for inline

**Span does not create a block**, it is an inline element, so ==do not use it to create a block separation== aka do not use it to take up region in x-axis/column. 
- Only use it to take up width not height. Do not stack it up and down, can only be stacked left and right. 
- If two span elements are side by side, semantically they should not be on top of each other like a stack, they need to be displayed side by side horizontally because they are inline elements. Use a div if you need the element to start next line.
- It's children also cannot be block(starts at the next line), its children can only be inline(starts within the line).
- Only use span if the element and its neighbors start inline and its children are all inline. 
- If inside a span has a div in a group of spans, then by definition it creates a second line and semantically does not make sense. Because a span by definition does not take up height and only takes up width as per its content.
- A span cannot take up height but it can take up size up to its parents size, ==solong as its all in one line, you can use span like a div.==




