Layout View nested in another layout view. Basically a Layout view with a layout view.
For example lets say we have this file called `_MasterLayout.cshtml`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>@ViewData["Title"] - My Application</title>
    <!-- Add your common CSS and script references here -->
    @RenderSection("Styles", required: false)
</head>
<body>
    <header>
        <h1>My Application</h1>
    </header>

    <div class="container">
        @RenderBody()
    </div>

    <footer>
        <!-- Add your common footer content here -->
    </footer>

    <!-- Add your common scripts here -->
    @RenderSection("Scripts", required: false)
</body>
</html>
```
The we have another Layout called `_HomeLayout.cshtml`.
```html
@{
    Layout = "_MasterLayout"; //set _MasterLayout as the Layout of _HomeLayout
}
<div>
	//specific code here fo home layout
</div>
```
This is rarely used, but it can be usefull if you think A master layout can DRY the other layouts.