These are not validations for the CORE Models, their validations are different.
These are only for the validations of the View Model/DTO, that will be used in the [[Strongly Typed Views]] **register view**, aka the **Sign-up page**.
These will be the most commonly used validation's for sign up.
# How-To:
- First, assuming you know how to make a [[Strongly Typed Views]].
- And assuming you know how to implement [[Client Side Validations tag helpers]].

Once you've created the view, create the `RegisterDTO`.
These are the most common validations and values for `RegisterDTO`:
```c#
 public class RegisterDTO
{
	[Required(ErrorMessage = "Name can't be blank")]
	public string PersonName { get; set; }
	
	[Required(ErrorMessage = "Email can't be blank")]
	[EmailAddress(ErrorMessage = "Email should be in a proper email address format")]
	[Remote(action: "IsEmailAlreadyRegistered", controller: "Account", ErrorMessage = "Email is already is use")]
	public string Email { get; set; }
	
	[Required(ErrorMessage = "Phone can't be blank")]
	[RegularExpression("^[0-9]*$", ErrorMessage = "Phone number should contain numbers only")]
	[DataType(DataType.PhoneNumber)]
	public string Phone { get; set; }
	
	[Required(ErrorMessage = "Password can't be blank")]
	[DataType(DataType.Password)]
	public string Password { get; set; }
	
	[Required(ErrorMessage = "Confirm Password can't be blank")]
	[DataType(DataType.Password)]
	[Compare("Password", ErrorMessage = "Password and confirm password do not match")]
	public string ConfirmPassword { get; set; }
}
```

Now simply use this DTO in your [[Strongly Typed Views]], and [[Client Side Validations tag helpers]] will automatically implement them in your sign-up/registration form.
