Filter for all the action methods of a controller class.
Creating the filter works exactly the same as in [[Action Filter]], the only difference is simply to move the `TypeFilter` to the controller so it is attributed to the controller class:
```c#
[TypeFilter(typeof(HomeControllerActionFilter))]
public class HomeController : Controller
{
	...
}
```