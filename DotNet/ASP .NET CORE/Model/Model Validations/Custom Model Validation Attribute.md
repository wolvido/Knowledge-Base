---
keywords: |-
  mvc how to validate two values at the same time
  mvc how to validate two properties at the same time
---
A custom validation for view models, if the requirement does not exist in [[Model Validations Attributes]].
Syntax:
```c#
class ClassName : ValidationAttribute
{
	public override ValidationResult? IsValid(object? value, ValidationContext validationContext)
	{
		//return ValidationResult.Success;
		// or return new ValidationResult("error message");
	}
}
```
##### Conventions:
- Custom model validation class should inherit from `ValidationAttribute`
- Last name should be `Attribute`.
- store in Models/CustomValidations as recommended.

Sample:
```c#
public class MinimumYearAttribute : ValidationAttribute
{
	public int MinimumYear { get; set; } = 2000; //by default if the user does not enter a MinimumYear
	//by default if the user does not enter an ErrorMessage in the model
	public string DefaultErrorMessage { get; set; } = "{0} should not be older than the year {1}"; 
	
	public MinimumYearAttribute() //allows us to add the attribute without parameters
	{  //empty here because this is the default constructor, we have default values above
	}
	
	public MinimumYearAttribute(int minimumYear) //overload so we can add a custom minimum year
	{
		MinimumYear = minimumYear;
	}
	
	protected override ValidationResult? IsValid(object? value, ValidationContext validationContext)
	{
		if (value == null) // value is the value of the property where the attribute is applied
		{
			return null;
		}
		
		DateTime date = (DateTime)value;
		if (date.Year > MinimumYear) //minimum is greater than because we are measuring date of birth
		{
			return new ValidationResult(string.Format(ErrorMessage ?? DefaultErrorMessage, validationContext.MemberName, MinimumYear));
			//we use string.Format as argument in validation result, so we can-
			//format-in the name of the property and the Minimum year (see string.Format note)-
			//this way {0} will be the name of the property and {1} becomes the minimum year.
			//we then create add a null coalesce of the ErrorMessage so if there is no error message in the attribute-
			//the default will be used
		}
		return ValidationResult.Success;
	}
}
```
>[!info] 
>Make sure you use this format: 
>**`return new ValidationResult(string.Format(ErrorMessage ?? DefaultErrorMessage, validationContext.MemberName, MinimumYear));`** 
>So it follows the convention and prevent confusion, Because the built in validation attributes has **`{0}`** as the property name.
>The code above ensures that **`{0}`** is the `validationContext.MemberName`.
>You can swap the `DefaultErrorMessage` variable to the string value if it is very short.

>[!warning]
>Just In case **`MinimumYear`** is of type **`DateTime`**, it will throw an error, convert **`DateTime`** or any type that is not easily converted to string, into string first. In sample case above `minimumYear` is of type **`int`**, it can easily be converted to its direct string type, no need to convert directly.

We can use the custom attribute above for this view model:
```c#
public class Employee
{
    [MinimumYear(2005, ErrorMessage = "Date of birth should not be newer than the year {0}")]
    DateTime? DateOfBirth { get; set; }
    //or
    [MinimumYear] //will work since we set it up with default values and empty constructor
    DateTime? DateOfBirth { get; set; }
}
```

> [!question] So what is the purpose of validation context?
It contains the context for the other properties that exist in the same view model.
One of its use is to be able to take data from two or more properties and apply an attribute to both or all at the same time. just like how the **[Compare]** attribute works. see [[Model Validations Attributes]] compare section.
#### Multiple value attribute
**Sample:**
```c#
public class CustomCompareAttribute : ValidationAttribute
{
    public string Property1 { get; }
    public string Property2 { get; }
 
    public CustomCompareAttribute(string property1, string property2)
    {
        Property1 = property1;
        Property2 = property2;
    }
 
    protected override ValidationResult IsValid(object value, ValidationContext validationContext)
    {
        // Your validation logic using Property1 and Property2
        // You can access the values of these properties through validationContext.ObjectInstance
 
        // For example, let's say you want to compare the values of Property1 and Property2
        var property1Value = validationContext.ObjectInstance.GetType().GetProperty(Property1)?.GetValue(validationContext.ObjectInstance, null);
        var property2Value = validationContext.ObjectInstance.GetType().GetProperty(Property2)?.GetValue(validationContext.ObjectInstance, null);
 
        if (property1Value != null && property2Value != null && property1Value.Equals(property2Value))
        {
            return ValidationResult.Success;
        }
 
        return new ValidationResult(ErrorMessage ?? "Property1 and Property2 do not match.");
    }
```
###### But If you want to create just simple validation without creating a custom validation attribute, You can use [[IValidateObject]].
An interface that allows you to implement custom validation logic at the view model itself.