instead of doing:
``` html
<input type="text" name="sample-name" id="sample-id" value="sample-value" etc..>
```
you can just do:
``` html
<input asp-for="model-property">
```
###### What it does?
Essentially it modifies the `<input>` tag to fit perfectly to the model property data type that you want to input.
Also used on `<textarea>`, `<select>`, and `<label>`.
# How-to:
All you have to do is add the model property name in the asp-for attribute on the input tag.
###### for example, you have the model:
```c#
public class CityWeather
{
	[Required]
	public int? CityUniqueCode { get; set; }
	[Required]
	public string? CityName { get; set; }
	[Required]
	public DateTime DateAndTime { get; set; }
	[Required]
	[Datatype(DataType.Password)] //notice we set the data type in the DataType attribute
	pubic string Password {get; set;}
}
```
And you want your `<form>` tag to receive a `CityWeather` and all its properties, so you do:
```html
<form>
	<input asp-for="CityUniqueCode" />
	//will automatically set the type as type="number" since it is int, will also set name="CityUniqueCode"
	//will also set a data-val="true" and data-val-rule since the property has [Required]
	
	<input asp-for="CityName" />
	//will set the type as type="text"
	
	<input asp-for="DateAndTime" />
	//will set the type as type="date"
	
	<input asp-for="Password" />
	//will automatically hide the characters when typed
</form>
```
It modifies the input tag to fit the model property and even its validation attributes is considered. see [[Client Side Validations tag helpers]]
#### Radio Input tag helper
It works the same, just repeat it. Sample:
```html
<fieldset>
    <div>
        <input asp-for="CashTransactionType" type="radio" name="CashTransactionType" value="Over-the-counter" />
        <label class="radio-controls__label">Over-the-Counter </label>
    </div>
    <div>
        <input asp-for="CashTransactionType" type="radio" name="CashTransactionType" value="Bank-pick-up" />
        <label class="radio-controls__label">Bank Pick-up </label>
    </div>
    <div>
        <input asp-for="CashTransactionType" type="radio" name="CashTransactionType" value="Online-transfer" />
        <label class="radio-controls__label">Online Fund Transfer </label>
    </div>
</fieldset>
```
>[!warning] VERY IMPORTANT
>##### When using tag-helpers on radio input, make sure that `asp-for` and `name` is the same, or else it will pass null data and not even validation can check it. Very weird oversight.
###### What is `[Datatype()]` attribute?
it adds metadata to the property so that tag helper knows how to design the frontend for that property.
Here is the list of all data types you can register in `[Datatype()]`: [DataType Enum (System.ComponentModel.DataAnnotations) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.datatype?view=net-8.0#fields)
#### asp-for
Its not only used in `<input>` tag it also used on `<textarea>`, `<select>`, and `<label>`.

On `<label>` it simply replaces `for` attribute of label with the name of the property. It helps to see typo since not existing properties will be marked red.
#### Model with data
If the action method supplies the view with a model with data, then the input will have a default value.
It will have `value="supplied-value"`.
#### Select tag helper
You can also generate the selections of the `<select>` dropdown tab and also dynamically generate it. see: [[Select tag helper]]
