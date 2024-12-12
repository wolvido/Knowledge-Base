The template view that is persistent in the page, the one that carries the header, footer, navbar etc..
>[!question]
>**What is it's purpose?**
>To dry the frontend, because most websites have the same header, footer, navbar etc..
##### File Structure:
this file is named `"_Layout.cshtml"`  
>[!note]-
>All views that are not served directly must be prefixed with an underscore "`_`".
>Except for View Components because view components are named default.
#### Store the file in the Shared Views Folder.
#### Notable uses:
- Attach the css link on it so you dont need to link css on every view.
- not just the css but the whole head to be shared.
- Also attach a global js.
#### Sample:
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="~/css/stylesheet.css" />
    <title>Title</title>
</head>
<body>
    <header>
        <nav>
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/about">Weather</a></li> //will run action method routed to "/about"
                <li><a href="/contact">Contact</a></li> //will run action method routed to "/contact"
                <li><a href="/product"></a>Products</li> //will run action method routed to "/product"
                <li><a href="/whatever"></a>Etc...</li> //etc..
            </ul>
        </nav>
    </header>
 
    <div class="container">
        @RenderBody() //this will be the content of the other views
    </div>
 
    <footer>
        <p>sample footer</p>
    </footer>
 
    <script src="~/js/site.js"></script>
</body>
</html>
```
**The `@RenderBody()` is where the view is applied.**
#### Connect the layout to a view:
before the layout can be used by a view, a view needs to know the layout path.
This needs to be added in the view, or in the [[_ViewStart.cshtml]].
```html
@{
    Layout = "~/Views/Shared/_Layout.cshtml";
}
```
#### What do I need to know after this?
- Code would be repeated if every view needs to set the layout code above. It should be set it in a [[_ViewStart.cshtml]].
- What if you need a specific layout for that one view only, or you need dynamically changing layouts depending on user actions? You use [[Dynamic Layouts]].
- After you've learned of dynamic layouts, what if I don't want whole layouts to dynamically change, what if I only need a section of a layout to change or just to add a js to this view only. You use [[Section Layout Views]].
- It is also possible to nest Layout Views, but is very rare. see [[Nested Layout Views]].