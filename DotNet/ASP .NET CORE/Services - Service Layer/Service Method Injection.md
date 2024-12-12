Injecting the service in a specific action method, instead of the whole controller.
>[!warning]
>In most cases this is not used.
# How?
Instead of injecting in the controller itself, inject it in the action method by adding the `[FromService]` attribute to the parameters:
```c#
public IActionResult Index ([FromService] ISampleService _sampleService)
{
	var sample = _sampleService.GetSampleWhatever();
	return View(sample);
}
```
basically works the same as controller injection but injected on action method instead. Will automatically inject like in the controller injection as long as you registered the service in program.cs.
