Will run this middleware when condition is met, skip if not. If condition is met and configure executed, will continue to execute normal pipeline.
syntax:
```c#
app.UseWhen(predicate, configure)
```
**Predicate** - predicate is of type`Func<HttpContext, bool>;`, that func accepts type HttpContext outputs a bolean, this is used for checking if condition is met.
**Configure** - is of type `Action<IApplicationBuilder>`, that action accepts type `IApplicationBuilder` and returns nothing, since its an action that is to be executed when predicate is true.

sample:
```c#
app.Use(async (HttpContext context, RequestDelegate next) =>
{
    await context.Response.WriteAsync("Middleware 1\n");
    if (1 == 1) await next(context);
});
 
app.UseWhen(context => context.Request.Path.StartsWithSegments("/admin"), //predicate returns true if path is set to admn
    applicationBuilder => //application builder is the parameter of action
    {
        applicationBuilder.Use(async (HttpContext context, RequestDelegate next) => //this is the action taken
        {
            await context.Response.WriteAsync("Admin Page\nUseWhen Activated\n"); //action
            await next(context); //another action
        });
    }
);

app.Use(async (HttpContext context, RequestDelegate next) =>
{
    await context.Response.WriteAsync("Middleware 2\n");
    if (1 == 1) await next(context);
});
```