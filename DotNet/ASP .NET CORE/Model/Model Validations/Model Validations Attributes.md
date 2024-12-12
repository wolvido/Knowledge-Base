All the attributes used in Model Validation
##### **[Required]**:
Will validate if property is null or empty. Means it must not be null or it will register an error.
>[!info] Note
>will only work with nullable types since all value types have a default value and will never be null even when empty value is provided.

Syntax: `[Required(ErrorMessage = "value")]`
Sample:
```c#
public class Book
{
	[Required(ErrorMessage = "{0} cannot be empty or null")]
	public int? BookId { get; set; }
	public int? Price { get; set; }
	public string? Author { get; set; }
}
```
if validation error occurs, will return: **`BookId cannot be empty or null`**.
**Note**: can only be set to `{0}` since there is only one value set in `bookId` property, and that is the its name.
##### **[StringLength]**:
Will Validate the string length.
Syntax: `[StringLength(int maximumLength, MininmumLenth = value, ErrorMessage = "value")]`
Sample:
```c#
public class Book
{
	public int? BookId { get; set; }
	public int? Price { get; set; }
	[StringLength(20, MinimumLength = 3, ErrorMessage = "{0} name should be between {2} to {1} characters") ]
	public string? Author { get; set; }
}
```
if validation error occurs, will return: **`Author name should be between 3 to 20 characters`**.
>[!tip]
>Notice we can set it to `{1}`, and `{2}` since there are now values in the property put in by the attribute. 
>`{1}`, and `{2}` is the `int maximumLength` and `MininmumLenth = value`.

>[!warning]
>`{0}` will always be the name of the property **EXCEPT** in a [[Custom Model Validation Attribute]].
##### **[MinLength] and [MaxLength]**:
Specifies the minimum and maximum length of a string or collection property.
- Example:
```c#
[MinLength(5, ErrorMessage = "Too short")]
[MaxLength(100, ErrorMessage = "Too long")]
public string Description { get; set; }
```
##### **[Range]**:
Will Validate the maximum and minimum numerical value.
Syntax: `[Range(int Minimum, int Maximum, ErrorMessage = "value")]`
Sample:
```c#
public class Book
{
	public int? BookId { get; set; }
	[Range(1,9999.99, ErrorMessage = "{0} cannot be less than ${1} or more than ${2}")]
	public int? Price { get; set; }
	public string? Author { get; set; }
}
```
##### **[EmailAddress]**:
Validates if its an email
Syntax: `[EmailAddress(ErrorMessage = "value")]`
Sample:
```c#
public class Employee
{
	[EmailAddress(ErrorMessage = "{0} Invalid, enter a valid {0}")]
	public string? Email { get; set; }
}
```
##### **[Phone]**:
Validates if its a phone Number
Syntax: `[Phone(ErrorMessage = "value")]`
Sample:
```c#
public class Employee
{
	public string? Email { get; set; }
	[Phone(ErrorMessage = "Invalid {0} number, enter a valid {0} number")]
	public string? Phone {get; set; }
}
```
##### **[Compare]**:
The values of this property should be the same as the other
Syntax: `[Compare(string otherProperty, ErrorMessage = "value")]`
sample:
```c#
public class Employee
{
	public string? Password {get; set;}
	[Compare("Password", ErrorMessage = "{0} should be equal to {1}")]
	public string? ConfirmPassword {get; set;}
}
```
##### **[RegularExpression]**:
validates using Regex
Syntax: `[RegularExpression(string pattern, ErrorMessage = "value")]`
Sample:
	at this point I think you already know how it works, extrapolate the sample.
##### **[Url]**:
Ensures that the property value is a valid URL.
Syntax: `[Url(ErrorMessage = "value")]`
Sample:
	at this point I think you already know how it works, you don't need a sample.
##### **[CreditCard]**:
Validates that the property value is a valid credit card number.
Syntax: `[CreditCard(ErrorMessage = "value")]`
Sample:
	at this point I think you already know how it works, extrapolate the sample.
##### **[ValidateNever]**:
explains itself

Sample of Combined Validations:
```c#
public class Book
{
    [Required(ErrorMessage = "{0} cannot be empty or null")]
    public int? BookId { get; set; }
 
    [Required(ErrorMessage = "{0} cannot be empty or null")]
    [Range(1,9999.99, ErrorMessage = "{0} cannot be less than ${1} or more than ${2}")]
    public int? Price { get; set; }
 
    [Required(ErrorMessage = "a {0} number is required")]
    [CreditCard(ErrorMessage = "a valid {0} number is required")]
    public int? CreditCard { get; set; }
 
    [StringLength(20, MinimumLength = 3, ErrorMessage = "{0} name should be between {2} to {1} characters") ]
    public string? Author { get; set; }
}
```

>[!tip] **But what if you don't want the display name to be `bookId` or `CredidCard` but instead Book ID and Credit Card**
you set the **`[Display]`** attribute, see sample below:
```c#
public class Book
{
    [Required(ErrorMessage = "{0} cannot be empty or null")]
    [Display(Name = "Book ID")] //name is set here
    //If error is caught, Book ID wil be registered as the property display name, instead of BookId
    //will return "Book ID cannot be empty or null" instead of "BookId"
    public int? BookId { get; set; }
}
```
**NOTE:** Display is not a Validation Attribute, It is a Different kind of beast altogether, with its own different properties.
In this example, the `[Display]` attribute is used to specify how the properties should be labeled in a user interface.
#### A complete list of validation attributes can be found in the [System.ComponentModel.DataAnnotations](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations) namespace.
###### Also see: [[Bind and BindNever]]
> [!tip]
>**If None of these attributes work**, create your own, see [[Custom Model Validation Attribute]].

