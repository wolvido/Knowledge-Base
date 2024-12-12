Filters for the entire project. 
Creating the filter works exactly the same as in [[Action Filter]], the only difference is to register the filter in `program.cs` so that it is attributed globally.
# How-To:
In your `program.cs` locate **`builder.Services.AddControllersWithViews();`** and inside add the lambda:
```c#
builder.Services.AddControllersWithViews(options => {
	options.Filters.Add<NameOfFilter>();
});
```
#### With arguments/parameters
if your filter needs parameters/arguments:
```c#
builder.Services.AddControllersWithViews(options => {
	options.Filters.Add(new NameOfFilter(argument1, argument2));
	//dont get confused, argument1 and argument2 are variables with data on it, or it can be hard coded
});
```
>[!warning] 
>Your filter might have injected a service or a logger or whatever injection, in that case you need to get it through the `builder.Services.BuildServiceProvider().GetRequiredService`.
###### For example your filter is using a logger:
```c#
builder.Services.AddControllersWithViews(options => {
	var logger = builder.Services.BuildServiceProvider().GetRequiredService<ILogger<NameOfFilter>>();
	options.Filters.Add(new NameOfFilter(logger, argument1, argument2))
});
```
Not just logger, you can get any service injected.