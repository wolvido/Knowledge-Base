>[!warning]
>This is an inexperienced opinion.
>But from what I've seen, especially on game codes, and on how dependency pyramid works, and on why they need a v2 instead of just updating v1, this is most probably how they do it.

So to create an OOP style software, first you have to create a MAIN large class, in MVC pattern that's the controller.

Then that you will construct the whole program on that main, BUT you will not implement it, you will simply design and construct the program there, what that means is that you will not implement the functionality, you will only design it by constructing what functionality you need, that means constructing interfaces and combining them in the MAIN without really adding how it functions, just the interface.

Then, you will implement these interfaces, the implementation is also the same as the MAIN in a way that you will also construct interfaces not functionality itself.

Then you will implement the interface of the previous implementation, and again and again, until a point where the smallest [[Single Responsibility Principle (SRP)]] class is left, that is where functionality is built.

So essentially a pyramid, just like how .NET does not allow you to create circular dependencies, it must always be a pyramid of dependencies.

==Unless of course== your program is not that complex, and that you only need one layer of functionality, and that the interfaces of the main is directly implementing functionality. You can have a small pyramid instead of artificially stretching it.

# This is old, refer to [[Clean Architecture]] instead.





