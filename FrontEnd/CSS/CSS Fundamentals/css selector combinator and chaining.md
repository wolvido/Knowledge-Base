#css 
keywords:
	css combinator selector eg. >, +, or just space " "
	css class combinations
	css > , + ,  ~, space 
	css what does two class mean
	css class chaining
##### just space:
```css
parent descendant {
  /* styles applied to all the descendant of the parent*/
  /* note: parent and descendant can be an element or a css class and it will function the same*/
}
```
essentially all child and grandchild of **parent** that is set as **descendant** will have the styles.
example:
```css
<parent>
  <descendant>This is selected</descendant>
  <div>
    <descendant>This is also selected</descendant>
  </div>
</parent>
```
style will be applied to all descendant.
##### arrow sign:
```css
parent > child {
  /* style is applied to only direct child element named child*/
}
```
this is different since it does not encompass all descendant, just the direct child.
##### plus sign:
```css
element1 + element2 {
  /* the style is applied to element 2 only if it is adjacent to element1*/
}
```
##### minus sign:
```css
element1 ~ element2 {
  /* selects all element2 that is a next sibling of element 1 not a before sibling*/
}
```
example:
```html
<element2></element2> not selected

<element1></element1>

<element2></element2> selected
<element3></element3> not selected
<element2></element2> selected
```
##### comma:
```css
selector1, 
selector2 {
  /* they both have the same style */
}
```
##### css class chain:
```css
.class1.class2{
/*the outcome will only occur when both class is called in the same element.*/
}
```
when class chaining, there should not be empty spaces in the middle. 

Note: any selector can be a class, an element, an Id etc...