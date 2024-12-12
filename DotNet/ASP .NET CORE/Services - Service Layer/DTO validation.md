Just like in models, DTO also needs to have its own attributes and validation.
>[!question] Why do we need to validate DTO is the model has its own validations?
>Because each layer is built to be decoupled/self-contained of each other, each layer needs to have its own validation.

This is different from view model validations in the controller. We cannot use model state here, model state is used only in the controller, we need to use **ValidationContext**.
# How to?
By creating a static helper validation class, like a custom model state class that also handles the errors.
#### Folder Structure and File Name
First, in your service class library add a folder named "Helpers".
Then create a the helper class name it "ValidationHelper".
#### Model Validation Method
Validation Helper should look like this:
```c#
public class ValidationHelper
{
	internal class ValidationHelper
	{
		internal static void ModelValidation(object obj)
		{
			ValidationContext validationContext = new ValidationContext(obj);
			List<ValidationResult> validationResults = new List<ValidationResult>();
			bool isValid = Validator.TryValidateObject(obj, validationContext, validationResults, true);
			
			if (!isValid)
			{
				throw new ValidationException(validationResults.First()?.ErrorMessage);
			}
		}
	}
}
```
>[!info]
>the method is internal because it should not be used outside the service layer, it is only for validating DTO's in the service.

Now All you have to do is call **`ModelValidation`** method to your services, like for example:
```c#
public class SampleService  : ISampleService
{
	public SampleType1 AddSomething(SampleType2 sampleInput)
	{
		//To validat the input, just add
		ValidationHelper.ModelValidation(sampleInput)
	}
}
```
All you need to do is add Validation attributes to type `SampleType2` and every validation error will be caught.