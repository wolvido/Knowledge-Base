---
keywords: Attribute Routing vs Conventional routing
---
For samples of Attribute Routing see [[Controllers]]

When will you prefer attribute routing over conventional routing?

In ASP.NET Core, you can define routes for your web application using either attribute routing or conventional routing. The choice between the two depends on the complexity and requirements of your application. Here are some scenarios where you might prefer attribute routing over conventional routing:

1. Fine-grained control: Attribute routing allows you to define routes directly on the action methods or controllers using attributes. This gives you more granular control over the routing behavior for specific actions. You can have different routes for different actions, making it easier to manage and understand the routing logic.
    
2. Controller-specific routes: With attribute routing, you can define routes specific to a controller by placing the routing attributes directly on the controller class. This is useful when you have actions that share a common route prefix, simplifying the route definitions.
    
3. Action-specific routes: In some cases, you may want to have multiple routes for a single action method. Attribute routing allows you to define additional routes for an action by adding multiple attributes on the same method.
	
1. Complex routing requirements: If your application has complex routing requirements, attribute routing can provide a more straightforward and concise way to handle those scenarios. You can use route parameters, optional segments, and custom route constraints directly in the attribute, making the routing logic more readable.

On the other hand, conventional routing can be more suitable for simpler applications with straightforward routing requirements. It relies on the route template defined in the Startup class, which makes it easier to see all the routes at once. It's a good choice when your application has a small number of routes and doesn't require fine-grained control over individual actions.

