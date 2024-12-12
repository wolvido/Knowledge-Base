#jQuery 
##### Selecting Elements by ID
```js
$( "#myId" );
```
##### Selecting Elements by Class
```js
$( ".myClass" );
```
##### Selecting Elements by Multiple Selector Types
```js
$("div#byID.byClass") //will select the div element that has both the ID and the Class
$("#byID.byClass") or $("div.byClass") //will also work without id, class, or element selector
```
##### Selecting Elements by Attribute
```js
$( "input[name='first_name']" );
```
##### Selecting Elements by Compound CSS Selector 
```js
$( "#contents ul.people li" );
```
see [[jquery chained selectors]] for more info.
##### Selecting Elements with a Comma-separated List of Selectors
```js
$( "div.myClass, ul.people" );
```
see [[jquery chained selectors]] for more info.

for the complete comprehensive see:
[jQuery Selectors (w3schools.com)](https://www.w3schools.com/jquery/jquery_ref_selectors.asp)

or try this:
[Selecting Elements | jQuery Learning Center](https://learn.jquery.com/using-jquery-core/selecting-elements/#selecting-elements-by-id)

some exampes:
[Live Demo: jQuery Select Element by Compound Selector (tutorialrepublic.com)](https://www.tutorialrepublic.com/codelab.php?topic=jquery&file=compound-selector)
