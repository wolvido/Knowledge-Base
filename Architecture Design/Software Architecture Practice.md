##### Service
- a service serves a single responsibility that you define to solve a business problem. 
- sample; business has a cart, so you make a:
	- CartService - with methods such as the CheckoutCart(), ValidateCart(), etc...
- The scope of a service depends on how you define the business problem, there can be two correct ways to do it, its more of an art, just keep in mind to balance cohesiveness and coupling.
- When designing a service, keep in mind the goal of a service is behavior, so more likely it will need one or more entities and will not make sense if it only has a dedicated entity. 
	- For example a CartService will more likely need  `Cart`, `User`, `PaymentMethod`, `Order`, etc...
