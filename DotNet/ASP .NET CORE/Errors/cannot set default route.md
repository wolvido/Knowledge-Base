If route "/" always goes for hello world then check for middlewares that force it. Maybe you forgot to remove the default:
```c#
app.MapGet("/", () => "Hello World!");
```