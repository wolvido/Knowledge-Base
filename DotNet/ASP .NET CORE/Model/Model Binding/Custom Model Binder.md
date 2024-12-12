Its a custom view model binding, see [[Model Binding]]. Basically it allows you to create a custom model binder that would bind whatever data sent from the frontend into a view model object. see [[Model]] for more info on model objects.
>[!question] **what is the purpose of a custom model binder if the built in model binder exists?**
Sometimes the incoming data might have a different name or it goes beyond what the built-in can handle like Date format that does not subscribe to the basic date format etc.. in these cases you will need a Custom Model Binder.

>[!Info]
>In real development, custom model binders are rare, only use when needed.
###### First the conventions:
- add a CustomModelBindinders folder under Controllers.
- add ModelBinder to the last name.
- on the custom model binding class, inherit from `IModelBinder`.
###### Sample:
Problem: The incoming data has a First Name and a Last Name, but the requirements require the first name and last name to be one. In the built in model binding, the first name and the last name would be treated as separate properties.
We solve this by using:
```c#
public class SampleModelBinder : IModelBinder
{
	Person person = new Person(); //the model output once binding is done
	
	public Task BindModelAsync(ModelBindingContext bindingContext)
	{
		//check if FirstName is empty
		if (bindingContext.ValueProvider.GetValue("FirstName").Length > 0)
		{
			//get the value of FirstName
			person.PersonName = bindingContext.ValueProvider.GetValue("FirstName").FirstValue;
			//check if LastName is empty
			if (bindingContext.ValueProvider.GetValue("LastName").Length > 0)
			{
				//Manipulate data here
				//get the value of LastName the contacenate with FirstName to become PersonName
				person.PersonName += " " + bindingContext.ValueProvider.GetValue("LastName").FirstValue;
			}
		}
		//Of course `PersonName` is not the only properties of a `person` class, just omitted for learning purposes. 
		//Other values can be added using the method above, if values are int or others, you may have to convert it.
		// person.Age = Convert.ToInt32(bindingContext.ValueProvider.GetValue("Age").FirstValue);
		
		//The data gathered from separate FirstName and LastName is binded into person.PersonName
		bindingContext.Result = ModelBindingResult.Success(person);
		return Task.CompletedTask;
	}
}
```



The sample above will return will bind `FirstName` and `LastName` into `PersonName`. It will return a `person` object with a full name `PersonName` into the action method that needs it:
```c#
public IActionResult Index(Person person)
{
	//codes to manipulate person object
}
```
>[!warning]
>IF other properties are not set in the custom model binder, they will not be registered. ALL PROPERTIES must be manually added see:[[Sample Custom Model Binder]]

> [!warning]
> **A custom model binder is not automatically registered, it needs to be registered before it activates. see below.**
#### Model Binder Provider
In order for Custom Model Binder to work it needs to have a Model Binder Provider.
**Conventions**:
- create Model Binder Provider class on the same folder as CustomModelBinder.
- the class must inherit from `IModelBinderProvider`.

In order to register the custom model binder in the sample above to the `Person` type:
```c#
public class PersonBinderProvider : IModelBinderProvider
{
	public IModelBinder? GetBinder(ModelBinderProviderContext context)
	{
		if (context.Metadata.ModelType == typeof(Person))
		{
			return new BinderTypeModelBinder(typeof(PersonModelBinder));
		}
		return null;
	}
}
```
The code above will register type `Person` as having a custom model binder of `PersonModelBinder`.
**That's not all**. You also have to register the provider in the builder.
add this in program.cs:
```c#
builder.Services.AddControllers(options => {
	options.ModelBinderProviders.Insert(0, new PersonBinderProvider());
});
```
After all that, every `Person` type in any action method will now accept separate FirstName and LastName.

**NOTE**: validation is handled by validation attributes. see [[Model Validations]] and [[Model Validations Attributes]]

This is guaranteed working as tested on nov 2023







