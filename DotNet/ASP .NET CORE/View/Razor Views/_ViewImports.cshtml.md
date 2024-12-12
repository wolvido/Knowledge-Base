Easier way to import models to the views.
So instead of doing this on the top of the view on every view:
```html
@using NameOfProject.Models
<!DOCTYPE html>
<html>
	//html code
</html>
```
Create a **`_ViewImports.cshtml`** and put `@using NameOfProject.Models` on there.
```html
@using NameOfProject.Models.ModelSubfolder
```
**The only purpose of `_ViewImports.cshtml` is to import common namespaces that will be used by all views**.
If using [[Clean Architecture]] then import the DTO namespace. for example: `@using ProjectName.Core.DTO.SubFolderMaybe`
## What folder to store `_ViewImports.cshtml`?
Wherever view folder you put `_ViewImports.cshtml`, it works there.
So for example, I put a ViewImports in the View folder, that means every import in ViewImports will affect all views.
Consequently, If I put ViewImports only into the Home folder, it will only affect all views in the home folder.
>[!tip]
>you can create multiple `_ViewImports.cshtml` in every folder.