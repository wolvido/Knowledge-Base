#css
this is a weird chromium bug for fieldset, it happens because the grandparent is also flex. You can fix this by adding a buffer div making fieldset a child of the buffer div.


https://stackoverflow.com/questions/28078681/why-cant-fieldset-be-flex-containers