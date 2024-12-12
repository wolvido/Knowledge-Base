```html
<button type="button" onclick="location.href='@Url.Action("MyAction", "MyController")'" />
```

If youre button is an input version, use:
```html
<input type="button" value="Create" onclick="location.href='@Url.Action("Create", "User")'" />
```