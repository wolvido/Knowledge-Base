---
keywords: html guide
---
#html 
![[Pasted image 20230830184832.png]]

##### layout what you know then figure out from this list to replace a div:
Sectioning/parts of an html  
Identify from which of these categories the unknown div or part of the html might belong to and use the link to find.

1. **metadata** - contains metadata about the page and where the page gets its content, scripts, or styles. Examples are: 
```html
<head>, <link>, <style>, and <meta>
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#document_metadata](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#document_metadata)

2. **sectioning root/body element** - it is *the* **``<body>``** element, its just the `<body>`.  The body includes all the page content except the metadata. Metadata is not page content.

3. **Content sectioning** - Outlines the logical sections of the page. These are the main parts that visibly outline the page. Example: 
```html
<main>, <nav>, <article>, <footer or header>, or <section> for a generic section.
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#content_sectioning](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#content_sectioning)

4. **Text content** - Elements to ==section the content==(not the words in the content). While content sectioning outlines the page into logical separation. Text content elements are defined on content inside the logical sectioning/outline. Example: 
```html
<blockqoute>, <figure>, <figcaption>, <li>, <ul>, <div>.
```
[US/docs/Web/HTML/Element#text_content](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#text_content)

5. **Inline text semantics** - elements that section and or style words, numbers, lines, sentence, or anything that affects a piece of text or links the text to other values. examples:
```html
<strong>, <cite>, <time>, <code>, <span>.
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#inline_text_semantics](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#inline_text_semantics)

6. **Image and multimedia** - for multimedia. Example: 
```html
<audio>, <img>, <video>
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#image_and_multimedia](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#image_and_multimedia)

7. **Embedded content** - Various content from external sources. Example: 
``` html
<iframe>, <embed>, <source>
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#embedded_content](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#embedded_content)

8. **SVG and MathML** - ``<svg>`` used to create scalable vector graphics(https://tinyurl.com/howToSVG) or embed an svg. ``<math>`` for creating math formulas.
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml)

9. **Scripting** - to add inline scripts or scripts for 2d shapes, or no scripts. example:
```html
<script></script>, <canvas>, <noscript>
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#scripting](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#scripting)

10. **Demarcating edits** - These elements let you provide indications that specific parts of the text have been altered. Example:
```html
<del>, <ins>
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#demarcating_edits](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#demarcating_edits)

11. **Table content** - for tables. Example: 
```html
<col>, <table>, <colgroup>
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#table_content](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#table_content)

12. **Forms** - anything related to submitting data or selecting data. Example: 
```html
<col>, <table>, <colgroup>
```
[HTML elements reference - HTML: HyperText Markup Language | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#forms)

13. **Interactive elements** - interactive elements built in html, where usually you need js to build interactivity. Example: 
```html
<details>, <summary>, <dialog>
```
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element#interactive_elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#interactive_elements)

14. **Web Components** - for custom elements. Examples: 
```html
<slot>, <template>
```
note: you need to learn more about web components.

some examples:
<article> Defines independent, self-contained content  
<aside> Defines content aside from the page content  
<details> Defines additional details that the user can view or hide  
<figcaption> Defines a caption for a <figure> element  
<figure> Specifies self-contained content, like illustrations, diagrams, photos, code listings, etc.  
<footer> Defines a footer for a document or section  
<header> Specifies a header for a document or section  
<main> Specifies the main content of a document  
<mark> Defines marked/highlighted text  
<nav> Defines navigation links  
<section> Defines a section in a document  
<summary> Defines a visible heading for a <details> element  
<time> Defines a date/time