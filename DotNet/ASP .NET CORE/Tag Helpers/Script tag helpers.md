Add this in case the project uses cdn.

**Two tags are used:**
- asp-fallback-test
- asp-fallback-src
the former is to test if the cdn exist, the latter is the fallback if the cdn does not.
for example:
```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js" asp-fallback-test="window.jQuery" asp-fallback-src="~/jquery-file-downloaded-locally"></script>
```
Whats happening here is `asp-fallback-test` uses "window.jQuery" as a condition to check, if window.jQuery exists then it returns true and fallback is not run. If it returns false then fallback is run.
#### SO, how do I know what to put in `asp-fallback-test=""`
Well it depends on what you need tested. Essentially the value in `asp-fallback-test` is a condition, like what you put in an `if()` bracket. So the fallback runs if it returns false. 
If you are using a library framework like jQuery or other, then essentially you have to read its documentation.
On jQuery's case, it create a global object called `jQuery`, since in js `window` is the object of the current window, so checking if `asp-fallback-test="window.jQuery"` means checking wether `jQuery` exists in the current window.

So essentially, create a condition or in cdn library cases like jQuery, read documentation or search or ask gpt or something.
In jQuery plugins, its usually as easy as `window.jQuery.pluginName`.
# Also
What if you want to use [[Layout Views]] to put the script tags, but you only want it to be loaded in some views not all views.
You use [[Section Layout Views]].