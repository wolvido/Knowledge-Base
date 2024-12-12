how much responsibility should a single service have? How big is the responsibility of a single service? If I need a service, how do I even begin to make one?
###### Answer:
- Well, in essence a service should be responsible for only one service.
- But there are also designs, in the samples we've seen, we are using resource centric design, where the design is based on a resource.
- Like for example the Employee resource, you make a **`EmployeeService.cs`**, the employee service will have the all the crud methods, and all the additional necessary methods for whatever the site needs employee related. Like for example it will have a SortBy method for the list of employee display.