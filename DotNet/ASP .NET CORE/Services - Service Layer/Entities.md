Entities is basically like a View Model (see: [[Model]]), but instead of used by the views and controller, this is only going to be used by the service. It's essentially the same as a view model. Harsha just calls them models. But we will differentiate here by calling them entities and storing them in Entities class library.
The Services must not use models used by the view, they must use a separate model/entity class library.
>[!question] why not use the same model as the view?
>Separation of concerns. The layers must be separated and must have no knowledge of each other. Service Layer must not rely on models from the presentation layer and vice versa, they must be interchangeable. see:[[Single Responsibility Principle (SRP)]].

> This is also where [[DbContext and DbSet]] are stored if you are not using [[Clean Architecture]].
# How-To:
Its the same thing as [[Model]] but we will create a separate class library called "Entities".
- Create a class Library project name it "Entities".
- All the models/entities you need for your services, and the DbContext, just create and store them there, **unless you're using [[Clean Architecture]]**.
- Then have your service create a dependency on "Entities".
>[!warning] Important
>Don't forget; for every model or entity, you need to add a **`ToString()`** override, so that when the object is called by a method that expects a string, it returns the string value of the model, not the name of the model itself. see:[[ToString Override]].
