This is like [[_ViewImports.cshtml]] but all it contains is setting layout code:
```cshtml
@{
    Layout = "~/Views/Shared/_Layout.cshtml";
}
```
See [[Layout Views]] for context.
The purpose is so you don't have to set every view with set layout code. All you have to do is create a view start to be shared by the views.

>[!note]-
>All views that are not served directly must be prefixed with an underscore "`_`".
>Except for View Components because view components are named default.
#### Folder structure:
the folder structure works the same as [[_ViewImports.cshtml]], If you put the view start on the view folder it affects all views, but if you want to override and have a different layout for a specific folder, then you can create another view start and put it in that specific folder and that will only affect that folder.
Basically wherever you put the view start file, it affects every view on that folder.
>[!question]
>What if you need a specific layout for a single view only, or you need dynamically changing layouts depending on user actions? You use [[Dynamic Layouts]].

