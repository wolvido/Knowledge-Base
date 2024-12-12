An interface that allows you to implement custom validation function at the model itself. Instead of creating a [[Custom Model Validation Attribute]]. **Note:** this is rarely used.
Sample:
```c#
public class Book : IValidatableObject
{
    public DateTime? PublishingDate { get; set; }
    public string? Genre { get; set; }
 
    public IEnumerable<ValidationResult> Validate(ValidationContext validationContext)
    {
        // if genre is empty and publishing date empty, will throw result error
        if (string.IsNullOrEmpty(Genre) && PublishingDate.HasValue == false)
        {
            yield return new ValidationResult(
	            "Genre or PublishingDate must have a value", new[] {nameof(Genre), nameof(PublishingDate)}
            );
        }
        // Add more validation logic as needed
    }
}
```
`ValidationResult` accepts two parameters: the error message and list of property with the associated error.

if you forgot about IEnumerable or yield, see [[IEnumerable T]]