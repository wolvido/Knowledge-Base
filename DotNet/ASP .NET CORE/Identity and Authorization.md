---
keywords: Identity asp net
---
ASP.NET Core Identity handles the user identity for login, signup, etc.. Built on top of EF Core.
![[Pasted image 20240328174816.png]]
###### The layer is composed of 5 parts from Controller to the Identity Database:
Don't get confused, it's the same layer separation like everything.
1. **Controller:** Self-explanatory, its just Identity system injected in the controller.
2. **[[Identity Manager]]:**  Its the [[Services - Service layer]] of the Identity system. It contains all the methods/business logic for the [[Identity Models]].
3. **Identity Store:** Identity Store is the repository layer. It is automatically created by the **IoC** when [[Registering Identity in IoC]]. So here are the signup, login, and every methods. Composed of the **`UserManager`** and the **`SignInManager`** services.
4. **Identity DbContext:** Self-explanatory, its the [[DbContext and DbSet]] of Identity.
5. **Data Source:** The database itself, with all the identity tables.
# How-To:
>notice it's all numbered, you will need pre-requisite knowledge starting from 1.
1. Lets start with the [[Identity Models]].
2. [[Registering Identity in IoC]].
3. [[@User object]] - its the User object of the currently logged in user. You can use it to check if the user is logged in or to know the name of the current logged-in user.
4. [[Validations for register form view model]] - most commonly used validations for sign-up.
5. [[Identity Manager]] - Its the [[Services - Service layer]] of the Identity system. It contains all the methods/business logic for the [[Identity Models]].
6. [[Sign-up Sign-in system]] - explains itself.
7. [[Authorization Policy]] - this is what prevents anyone from accessing a certain page without logging in or signing-up.
7. [[Return URL]] - If the user fails to access a link because of not being signed-in, after signing-in it will automatically redirect to the failed link.
8. [[Remote Validation]] - Validate if username or email already exists without accessing the database. Saves resource and page refresh.
9. [[User Roles]] - There are user roles like Customer Role, Admin Role, Employee Role etc.. Identity has built in service methods and database to register and manage the roles.
10. [[Areas]] -  You need to learn this as a pre-requisite to [[Role Authentication]]. 
11. [[Role Authentication]] - You already know there are [[User Roles]]. We can authenticate pages, pages where only the customer role or the admin role should be able to access, the pages are separated using [[Areas]].
12. [[Custom Authorization Policies]] - In rare instances, you might need an even more complex authentication than [[Role Authentication]], like for example you want to make a controller inaccessible if the user is logged in.
13. [[XSRF]] - To protect against Identity attackers.