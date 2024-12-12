handling form validation errors that prevent users from entering from values into a view form.
![[invalid-form.png]]
There are two ways to handle it, you can handle it manually or you can simply use:
[[Client Side Validations tag helpers]].

I strongly suggest simply using [[Client Side Validations tag helpers]], no need to reinvent the wheel.
But if you really need to do it manually:
# Manual method:
- Assuming we are creating a register account system.
- Assuming you've already set up the view form and you've connected it to the controller.
- Assuming you already now how checking the `ModelState` works, if not see: [[Model validation error handling]].
###### Controller:
```c#
[HttpPost]
public IActionResult Register(RegisterDTO registerDTO)
{
	//check for validation errors
	if (ModelState.IsValid == false)
	{
		ViewBag.Errors = ModelState.Values.SelectMany(temp = temp.Errors).Select(temp => temp.ErrorMessage);
			//register all the validation errors and send it to viewbag
		return View(registerDTO);
	}
	
	//No error code here...
}	
```
Then simply have the view display the error messages.

