#js
 in cshtml:
``` html
<script>
    var transactions = '@Html.Raw(System.Text.Json.JsonSerializer.Serialize(Model))';
</script>
```
 in js:
```js
 var transactions = JSON.parse(window.transactions);
```

There are many other ways like using ajax, but this is the way I found to be most simplest in my opinion since I dont have to create a separate action method, I can just pass the model to the original action method. I just have to serialize it in the view.

I don't even know yet why anyone uses ajax.