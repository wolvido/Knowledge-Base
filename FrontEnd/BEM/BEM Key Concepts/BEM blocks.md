#bem 
Block is a self contained reusable component.
It is considered a block if it has a self contained style or functionality.
A block can be as small as a `button` or `logo`.
###### How to name a block?
- The [block name](https://en.bem.info/methodology/naming-convention/#block-name) describes its purpose ("What is it?" — `menu` or `button`), not its state ("What does it look like?" — `red` or `big`).

- a block should be positioned by its parent, the parent should encompass and not require a positioning. see [[how to position blocks]]
  
- blocks in a mixed should be positioned by creating an element alongside the block and setting the position in the element.

- You can nest a block inside a block or alongside each other:
```html
  <!-- `header` block -->
<header class="header">
    <!-- Nested `logo` block -->
    <div class="logo"></div>

    <!-- Nested `search-form` block -->
    <form class="search-form"></form>
</header>
```