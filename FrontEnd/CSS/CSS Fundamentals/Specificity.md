#css
keywords:
	css priority order
	css specificity heirarchy

Specificity is an algorithm that calculates the weight that is applied to a given CSS declaration. The weight is determined by the number of [selectors of each weight category](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#selector_weight_categories) in the selector matching the element (or pseudo-element). If there are two or more declarations providing different property values for the same element, the declaration value in the style block having the matching selector with the greatest algorithmic weight gets applied.

![[Pasted image 20230731211018.png]]

[Specifics on CSS Specificity | CSS-Tricks - CSS-Tricks](https://css-tricks.com/specifics-on-css-specificity/)