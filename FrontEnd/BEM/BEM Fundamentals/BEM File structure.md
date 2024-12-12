#bem 
extend the width of the screen if it is confusing
```
project 
    common.blocks/                            # Redefinition level with blocks 
        input/                                # Directory for the input block 
            _type/                            # Directory for the input_type modifier 
                input_type_search.css         # CSS implementation of the input_type modifier 
            __clear/                          # Directory for the input__clear element 
                _visible/                     # Directory for the input__clear_visible modifier 
                    input__clear_visible.css  # CSS implementation of the input__clear_visible modifier 
                    
                input__clear.css              # CSS implementation of the input__clear element
                input__clear.js               # JavaScript implementation of the input__clear element 
        input.css                             # CSS implementation of the input block 
        input.js                              # JavaScript implementation of the input block
```
[https://en.bem.info/methodology/filestructure/#nested](https://en.bem.info/methodology/filestructure/#nested)
common.block is a  redefinition level.

#### Always remember:
create [[redefinition levels]] for your blocks