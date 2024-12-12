Sometimes the images in the client side does not update to the changes made by the server because the client uses cache version. If you have an image that needs to be updated soon as possible like a logo use tag helper `asp-append-version`.
sample:
```html
<img src="~/FilePath" asp-append-version="true"/>
```
will now update the image every time the server changes, and the client will still use cache if necessary, there is a hashcode that the client uses to check whether there's changes or not.