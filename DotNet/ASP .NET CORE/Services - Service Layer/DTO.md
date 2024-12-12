---
keywords: |-
  View model 
  This is essentially view model
---
DTO are **Data Transfer Object**, it is used to transfer data without exposing domain models/models of the business logic. It is what Harsha uses as view model. It is usually used to transfer from service layer/business layer to presentation layer (controller) and vice versa.
>[!question] Why use DTO?
> Essentially it helps to encapsulate one layer from other layers. 
> - see: [[What's the point of DTO's]]?
> - see:  [Should services always return DTOs, or can they also return domain models?](https://stackoverflow.com/questions/21554977/should-services-always-return-dtos-or-can-they-also-return-domain-models) and [Can we use only DTO instead of ViewModel?](https://stackoverflow.com/questions/50576894/can-we-use-only-dto-instead-of-viewmodel)
#### Sample:
Lets say you have a **`CountriesService.cs`** that uses the **`Country.cs`** model/entity.
```c#
public class Country
{
	public Guid CountryId {get; set;}
	public string? CountryName {get; set;}
}
```
This domain Model/Entity **MUST NOT BE EXPOSED** outside the business layer/service layer. 
It must not be exposed to the controller, since the controller is part of the presentation layer.
>[!note]
>If you're confused about the definitions, see: [[DTO vs Model vs domain objects vs entities]].
# So how to communicate if you cant expose a model?
By making DTO equivalents and DTO methods.
![[Capture 37.png]]

- In this note we will focus on creating a DTO method for **adding** and **response**, once you learn how to make Adding and general response DTO method, you can extrapolate in creating a DTO for every use case.
- In this note we will also assume we are working on a **`CountriesService.cs`** service class.
#### First The Folder Structure
In the same class library as the **service contracts**, create a DTO folder. Store DTO's there. Name the folder "DTO".
The **Service Contracts Library** is the one were you put the interfaces in, not the service class library. see [[Services - Service layer]].
- If using Clean architecture, the DTO folder should be in the Core itself. [[Core Layer]].
#### Naming Convention
When creating a DTO method, the input DTO type must be postfixed with "Request" and the output must be postfixed with "Response". 
Sample:
```c#
public CountryResponse AddCountry(CountryAddRequest? countryAddRequest)
{
	...
}
```
#### AddRequest DTO
First we will create a `CountryAddRequest` DTO, this will be used as the input when adding a model `Country` instead of using `Country` model, which the controller does not know of. `Country` model should not be exposed to the controller and should only be used in the service layer.
```c#
public class CountryAddRequest
{
	public string? CountryName {get; set;}
	//It does not contain the GUID property since GUID must be uniquely generated from the model
	
	//Then we create a ToCountry() method for this DTO, because since CountryAddRequest is-
	//used as the input, we need convert it To a Country model to be used by the service.
	public Country ToCountry()
	{
		return new Country()
		{
			CountryName = CountryName,
			//the first CountryName is from Country model, the second one is from this DTO
			//We assign CountryName from the DTO to the Country Model
			//make sure to import the Country model or this will not make sense
		};
	}
}
```
#### Response DTO
Create a Response DTO.
This will be used as the return type, instead of exposing the Domain model.
```c#
public class CountryResponse
{
	public Guid CountryId {get; set;}
	public string? CountryName {get; set;}
	//
}
//this code file is not finished yet
```
**Pay attention here** this maybe a bit complicated and appear weird at first, but makes good sense.
- Previously on `CountryAddRequest` class, we created a `ToCountry()` because we need to convert the input DTO class `CountryAddRequest` into `Country` Model, so the service can use `Country` Model.
- But, `CountryResponse` is an output, so when sending an output, we need to convert `Country` Model again into a `CountryResponse` DTO class. 
- Similar to how we add a `ToCountry()` method to `CountryAddRequest` DTO. Now we create a `ToCountryResponse()` method to convert `Country` into `CountryResponse`.
- So here is the bit weird but makes good sense part. We cannot directly add a `ToCountryResponse()` to `Country` Model just like how we add `ToCountry()` in `CountryAddRequest`, that would not make sense since it will breach layer separation.  This will give the domain entity knowledge outside of domain layer and break the dependency hierarchy.
- So how do we add a method to `Country` without breaking the dependency hierarchy?
##### By creating an extension method
This extension method will be in the same file as `CountryResponse` DTO class, just below the enclosure of `CountryResponse` class. 
```c#
public static class CountryExtensions
{
	public static CountryResponse ToCountryResponse(this Country country)
	{
		return new CountryResponse() 
		{
			CountryId = country.CountryId, 
			CountryName = country.CountryName
		};
	}
}
```
see: [[Extension Methods]] for info if you forgot.
#### Service Method
Now we implement the service and the method that adds a country in the database.
Since `Country` model cannot be exposed, `countryAddRequest` DTO will be used as input and `CountryResponse` as output.
```c#
public class CountriesService : ICountriesService
{
	public CountryResponse AddCountry(CountryAddRequest? countryAddRequest)
	{
		//here we use ToCountry method to convert CountryAddRequest to Country
		Country country = countryAddRequest.ToCountry();
		
		//here we generated the GUID for the new country
		country.CountryID = Guid.NewGuid();
		
		//Add Country to the database
		CountryDatabase.add(country); 
		//WARNING this is just sample code of adding it to the database, this is not really how you add
		//how you add to the database depends
		
		//convert the model to the output DTO
		return country.ToCountryResponse();
	}
}
```
>[!Warning]
>Of course keep in mind there needs to be validations, this is just the barebones for the service, in real world there needs to be validation. Use Attribute Validations on the DTO properties see: [[DTO validation]].
#### Conclusion
So in this note we created a DTO method for Adding a country, once you learn how to make Adding DTO method, you can extrapolate in creating an Update DTO method, Delete DTO method, Get DTO, etc..
Heres a **GetAllCountries** example to give you an idea:
![[Capture 38.png]]
There is an exception to the no exposing model rule, that is if the data exposed is a native type or a universal type, like string, int, or GUID. 
Here is an example of passing a countryId of type GUID:
![[Capture 39.png]]
The important thing is that the controller does not know anything about the domain model/entity.
Most services need to have Get, Update, Add, Delete methods, Basically the whole CRUD.

==Essentially DTO's are the properties to a class, and the entities are the fields==
 see: [Should services always return DTOs, or can they also return domain models?](https://stackoverflow.com/questions/21554977/should-services-always-return-dtos-or-can-they-also-return-domain-models) and [Can we use only DTO instead of ViewModel?](https://stackoverflow.com/questions/50576894/can-we-use-only-dto-instead-of-viewmodel).
##### ==How do I know what DTO to make?==
Design it per use case.
- so if you have a use case where you want to update a country, create a `CountryUpdateRequest` DTO.
- If you need to display a country, make a `CountryResponse` DTO.
- If you want to add a country, make a `CountryAddRequest` DTO.
- It is any use case like: `OrderDetailsResponse`, `OrderItemResponse`, `CreateOrderRequest`, `CreateOrderResponse`, literally anything that needs a request to the server and a response. It's ok to reuse DTO of course, but make a new one if one use-case requires more or less properties.
This approach makes it easier to maintain and update your code since changes in one use case or endpoint will not inadvertently affect others. see: [[What's the point of DTO's]].
==But for simple use-cases, anything that only needs one property like a delete use case, you don't need to make a DTO.== 
- For a delete operation, you only need a service that accepts the Id or a single property.
- Or do what harsha does and grab the ID from update DTO.
>[!important]
>Don't get confused, you only need to create DTO's per-use case that have different properties from the each other, so its ok to reuse DTO if the Use-case can use the same DTO.
#### View Model DTO
This is a different kind of DTO, this DTO is only used for, [[Strongly Typed Views]], since they need their own models, so you need to make one.
Don't get confused with needing a view model, DTO is what harsha uses as view models. 
Essentially this is used to send data from view to the controller, make a view DTO that is only for the transfer of data from View to Controller. If using [[Clean Architecture]], you can store this DTO in the [[UI Layer]].
Naming convention: just suffix it with "DTO" or "Dto" depending on the project.
>[!warning]
>Harsha doesn't use view models, he just uses the DTO from Core. Maybe we don't need a this.
###### How-To:
1. How this works is you create the DTO's to be used by [[Strongly Typed Views]]. Imagine you need to register an account, so you create a `RegisterDTO` with username and email as its properties.
2. Then you use it to send data from view to controller:
```c#
[HttpPost]
public IActionresult Register(RegisterDTO registerDTO) //registerDTO binds the data from a "register" form.
{
}
```
3. Then when you're done making the service layer/core layer and its own DTO's,  map the view DTO into the core DTO via the controller:
```c#
[HttpPost]
public IActionresult Register(RegisterDTO registerDTO) //register DTO binds the data from a register form view.
{
	AccountRequest accountRequest = new AccountRequest() {UserName = registerDTO.Username, Email = registerDTO.Email};
	
	//the send the request DTO to a service method
	AccountResponse accountResponse = _accountService.AddAccount(accountRequest);
}
```

Now this way UI layer has no knowledge of the service layer, and you can also develop them independently, you only need to map it later.
#### What next?
- We also need to validate the data in DTO. see [[DTO validation]].






