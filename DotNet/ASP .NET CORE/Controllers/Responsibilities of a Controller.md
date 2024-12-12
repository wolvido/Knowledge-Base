---
keywords: |-
  What exactly should a controller do 
  What action methods should be inside a controller?
---
The Controller is the one the controls the data, moves the data, passes the data. It is not the source of data or the receiver of data. It is the controller.
###### So what action methods should a single Controller have? How do I group action methods?
1. **Single Responsibility Principle (SRP):**
Each controller should ideally have a single responsibility. It should be responsible for handling a specific set of related actions or a specific area of your application. For example, you might have a `UserController` to handle user-related actions, an `OrderController` for order-related actions, etc.

2. **Resource or Entity-based Design:**
Organize controllers based on the resources or entities they represent in your application. If your application deals with users, orders, and products, create controllers like `UserController`, `OrderController`, and `ProductController`. Actions within each controller should then relate to the CRUD operations for that resource.
This is what Harsha uses.

3. **Action Semantics:**
Group actions that share similar semantics. For instance, actions related to displaying views might be grouped together in one controller, while actions related to handling AJAX requests might be in another.

4. **RESTful Principles:**
If you are following RESTful principles, organize your controllers around the resources of your application. For example, if you have a resource like "employees," you might have an `EmployeesController` with actions for creating, updating, deleting, and listing employees.

5. **Controller Size:**
Avoid having overly large controllers with too many action methods, consider breaking it down into smaller, more focused controllers. This promotes better maintainability and readability.

6. **Areas:**
Use areas in ASP.NET MVC to organize controllers further, especially if your application has distinct functional areas. For example, you might have an "Admin" area with controllers for administrative tasks and a "User" area for user-related functionality.
##### So to answer the question: it depends on the design.
---
![[res.png]]

