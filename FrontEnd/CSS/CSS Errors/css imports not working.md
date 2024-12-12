#css 
it might be because the first import overrides the second in line.

Also in nested imports, the current file overrides the imported regardless of line position.

make sure you use **singleqoutes** `@import url('sample.css');`

Or probably you just forgot the dot in front of a css class.