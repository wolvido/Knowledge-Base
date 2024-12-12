---
keywords: |-
  how to render view with data and path
  how to pass model to view and have manual path
---

```c#
return View(); //will use the default path and no model is passed
return View(model); //will use the default path and pass model data to the view
return View("index"); //disregard default file name and use the file named index.cshtml and no model data is passed to the view
return View("index", model); //disregard default file name and use the file named index.cshtml and pass model data to the view
```