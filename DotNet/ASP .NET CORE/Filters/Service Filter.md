It is exactly the same as **`TypeFilter`** but without arguments. It's here just in case you encounter it, but you can forget about it in general
###### Instead of this:
```c#
[TypeFilter(typeof(FilterClassName))]
public async Task<IActionResult> Index()
{
	//codes...
}
```
###### You can swap for this:
```c#
[ServiceFilter(typeof(FilterClassName))]
public async Task<IActionResult> Index()
{
	//codes...
}
```
The only difference is `TypeFilter` can get arguments, see: [[Filter with arguments]].
###### If by any chance you want to use service filter, then you will need to register it in the IOC.
just like you add any other service:
```c#
builder.Services.AddTransient<SampleActionFilter>(); //of course you can use other scope also, trasient is just a sample
```