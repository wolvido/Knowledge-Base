---
keywords: "\t# BEM block folders  \t# BEM folders  \t# how bem divides its files"
---
#bem 
###### Redefinition levels are levels that extend, add new property, or redefine BEM blocks.
Redefinition levels are used for the following purposes:
- [To add new blocks to a project](https://en.bem.info/methodology/redefinition-levels/#adding-blocks-to-a-project)
- [To change existing blocks](https://en.bem.info/methodology/redefinition-levels/#changing-the-block-implementation)
You can create any redefinition levels, as long as its convenient. It acts like a level for modifying or extending blocks, for example:
![[Capture 54.png]]
It changes for every level, depending on your styling needs.
![[Pasted image 20240607181854.png]]
###### It's not limited to adding properties, you can also redefine a block, for example:
- The button block in CSS on the library.blocks level:
```css
.button { 
    position: absolute; 
    border: 1px solid rgba(0,0,0,.2); 
    border-radius: 3px; 
    background-color: #fff;
}
```
Then create another `button` block on the `common.blocks` project level and place the `button.css` file in it with the new button styles.
- The button block in CSS on the common.blocks level:
```css
.button {
    background-color: #ffdf3a;            /* New button color */
    width: 150px;                         /* Button width */
    box-shadow: 0 0 10px rgba(0,0,0,0.5); /* Shadow parameters */
}
```
The implementation of the `button` block will consist of the original CSS rules from the `library.blocks` level and the additional rules from the `common.blocks` level:
```css
@import "library.blocks/button/button.css";  /* Original CSS rules from the library level */
/* override library with common */
@import "common.blocks/button/button.css";   /* Properties from the common.blocks level*/
```
---
#### **The most common redefinition levels are the:**
##### `/common.blocks`
This level holds reusable blocks that are specific to your project but might be used across different parts of your application. These blocks is not necessarily a part of a shareable library.  The main thing is that they are shared by the whole project.
##### `/library.blocks` 
These blocks sourced from a library or framework and provide base styles and functionality. They are intended to be more general-purpose and not specific to any one project.
###### What Should Be Contained in `library.blocks`?
1. **Generic Components**:
    - Basic UI components that can be reused in multiple projects such as buttons, inputs, modals, forms, grids, etc.
    - Example: `button/`, `input/`, `modal/`, `grid/`.
2. **Framework Blocks**:
    - Blocks that come from external libraries or frameworks (like Bootstrap, Foundation, etc.).
    - Example: `bootstrap-grid/`, `foundation-button/`.
3. **Utility Classes**:
    - Helper classes that provide common CSS utilities.
    - Example: `clearfix/`, `text-center/`, `margin/`.
4. **Vendor Code**:
    - Any third-party code or libraries that are included in your project.
    - Example: `normalize.css/`, `jquery/`.
5. **Icon Libraries**:
    - Reusable icons or icon sets.
    - Example: `font-awesome/`, `material-icons/`.
---
##### So when should I use Redefinition Levels?
###### They are most commonly used in:
- **Platform Redefinitions:**
```
project/ 
    common.blocks/ 
        button/ 
            button.css   # basic CSS button implementation 
    desktop.blocks/ 
        button/ 
            button.css   # custom button for desktop 
    mobile.blocks/ 
        button/ 
            button.css   # custom button for mobile
```
- **Theme redefinitions**
  You can also add different themes as redefinition:
```
project/ 
    common.blocks/  
        button/ 
	        button.css 
    desktop.blocks/ 
        button/ 
            button.css 
    ...
    alpha/            # alpha design theme 
        button/ 
    beta/             # beta design theme 
        button/ 
```
###### For more redefinitions see: [Redefinition level / Methodology / BEM](https://en.bem.info/methodology/redefinition-levels/#dividing-a-project-into-platforms)

