Service is a class that contains the business logic. This is where the business logic should be.
The service is in the middle of the presentation layer and the data layer. It calculates and validates, from the data layer to be sent to the presentation layer. Presentation layer is the controllers and views.
>[!note]
>What is IoC or DI?
>see:[[IoC]]
# How-to:
#### First, Naming Convention
Suffix any service class with "Service", for example:
- `CitiesService`, `ICitiesService`
- `StudentsService`, `IStudentsService`
- `EmployeesService`, `IEmployeesService`
#### Create two separate library
- Create separate class libraries to store the services in, as good practice. 
>[!tip]- If you dont know how
right click on solution, then add, then new project, then search for class library
- No strict convention for naming the class library, you can name it anything as long as it is appropriate.
- In this example we will simply name the services Library as **"Services"** and the service interfaces as **"ServiceContracts"**.
- create a class library named as **"Services"** to store the service and another one as **"ServiceContracts"** to store the service interface.
- You can also create a separate "Models" class library if necessary.
###### - If using [[Clean Architecture]], disregard all of the above and create "ServiceContracts" and "Services" folder in the src.
#### Create the Service Abstraction AKA Interface for the Service
We cannot directly use an object of the Service in the controller, that would break the [[Dependency Inversion Principle (DIP)]]. So instead we need to implement an abstraction first, so we can inject it, see: [[Dependency Injection]].
- In this note, we will use a **`ShoppingCart`** business logic/service.
Inside the **''ServiceContracts''** library project create `IShoppingCartService` interface:
```C#
// Interface for the service
public interface IShoppingCartService
{
    decimal CalculateTotalPrice(List<decimal> itemPrices);
}
```
#### Create a Service class under the Services class library
- First, add the "ServiceContracts" into "Service" dependencies, so we can import `IShoppingCartService` into the service.
>[!tip] How to Add dependencies?
>Under Services, right click dependencies, select add project reference, look for "ServiceContracts", then check.

The we create the service implementation class. 
This Class will be put in the "Services" class library project made earlier.
```c#
using ServiceContracts; //dont forget to import ServiceContracts

public class ShoppingCartService : IShoppingCartService
{
    public decimal CalculateTotalPrice(List<decimal> itemPrices)
    {
        // here we add the logic for calculating total price of the shopping cart
        // or maybe also appllying discounts based on certain criteria etc
        decimal totalPrice = itemPrices.Sum();
        
        return totalPrice;
    }
    
	//CalculateTotalPrice is just one sample of a service method.
    //Of course we also add all the necessary CRUD methods in the Service.
    //for example we also add a AddItem method, DeleteItem etc..
//Not just CRUD methods, every other business logic necessary in handling the data it handles, in this case ShoppingCart
}
```
>[!info]
>Interface are designed to be extensible of course, implementation of `IShoppingCartService` doesn't necessarily need to be `ShoppingCartService` it can also be `DatabaseShoppingCartService`, or `InMemoryShoppingCartService`,  or any specific implementation.
#### Add Dependencies and Register the Service
- Before we can register the service and the service abstraction, we need to add both "Service" and "ServiceContracts" into the main project's dependencies.
>[!tip] How to Add dependencies?
>same as last time, Under ProjectName, right click dependencies, select add project reference, look for "ServiceContracts" and "Services", then check both.

Register the service in program.cs, by adding:
```c#
using Services; //dont forget to import these both
using ServiceContracts;

builder.Services.AddTransient<IShoppingCartService, ShoppingCartService>();
// or
builder.Services.AddScoped<IShoppingCartService, ShoppingCartService>();
// or
builder.Services.AddSingleton<IShoppingCartService, ShoppingCartService>();
```
Notice I put **or**, that's because you only need to use one, either `AddTransient`, `AddScoped`, or `AddSingleton` depending on what is required. 
>[!question]
>Which one should I choose and what does it mean?
see: [[Transient, Scoped, Singleton]].
#### Now, use it in the controller
```C#
public class ShoppingCartController : Controller
{
	//field for the injection
    private readonly IShoppingCartService _shoppingCartService;
    
	// Controller Constructor accepts a type IShoppingCartService so we can inject our-
	// ShoppingCartService Service
    public ShoppingCartController(IShoppingCartService shoppingCartService)
    {
        _shoppingCartService = shoppingCartService;
        //The IoC will automatically inject a shoppingCartService object to- 
        //shoppingCartService argument and be assigned to _shoppingCartService field
    }
    
    public IActionResult CalculateTotal()
    {
        // Dummy data for item prices
        List<decimal> itemPrices = new List<decimal> { 10.5m, 20.75m, 5.0m };
        //of course the data should be from server, this is just for sample
        
        // Use the service to calculate the total price
        decimal totalPrice = _shoppingCartService.CalculateTotalPrice(itemPrices);
        
        // You can then use the totalPrice in your view or return it as needed
        return View(totalPrice);
    }
}
```
So, you might be wondering how this will work if we never injected anything in the controller?
Well yes we did, that's the purpose of this code in the program.cs:
```C#
builder.Services.AddTransient<ICitiesService, CitiesService>();
```
It Automatically injects `CitiesService` to the controller if the controller asks for an `ICitiesService` .
>[!warning] Important
>You can inject a service into another service just like you would in the controller. Just make sure you don't create a Captive Dependency. see [[Best Practice for Services and DI]] for more info on Captive Dependency.
# What next?
- What if you need to reference a Model/Entity in your Services? You create another separate class library for your Models/Entities. See: [[Entities]]. The Services must not use models used by the view, they must use a separate model/entity class library. The same principle applies to other layers, it is good practice to separate the layers, that is why we separated the Services and the ServiceContracts. 
- [[how big is a service layer]]? how much responsibility should a single service have? If I need a service, how do I even begin to make one?
- There also this thing called DTO, where it is used by the service to transfer data, essentially a view model, In the sample above we transferred a decimal type. We need to use DTO for encapsulation. see [[DTO]].
- What if you don't need the service for the whole controller, what if you just need to inject the service in one action method only. See: [[Service Method Injection]]. But in most cases this is not used because its not extensible to other action methods.
- [[Transient, Scoped, Singleton]] read this if you haven't already.
- Just like how you can inject the services into the controller or other service, You can inject the service into a view as well. see [[View Service Injection]].
- Best Practices for Services and Dependency Injections [[Best Practice for Services and DI]].
- What if you need a another scope **inside** the service that is separate from [[Transient, Scoped, Singleton]] . Instead of waiting for the whole service to be destroyed by Transient, Scoped, or Singleton scope. For example your service creates a DB connection and that DB connection needs to be destroyed when its done being used instead of waiting for Transient, Scoped, or Singleton scope. See [[Service Scope]]. **But this is not needed if you are using entity framework core.**
- What if `program.cs` is filled with service registrations and it becomes unwieldy? [[Arrange Program.cs]].
- **Autofac** is an open source alternative to the IoC Container. see [[AutoFac]]. It is not required to use this, best practice is to use default, then when you think the default cant handle the requirements, use Autofac, if you think Autofac cant handle, then use those even more advanced than Autofac.
- What if your service needs to access the database? you use a [[Repository]] and an ORM framework like [[Entity Framework Core]].
