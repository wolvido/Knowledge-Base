#cSharp 
**According to msdn:**
##### Use a delegate in the following circumstances:
- An eventing design pattern is used.
- It is desirable to encapsulate a static method.
- The caller has no need to access other properties, methods, or interfaces on the object implementing the method.
- Easy composition is desired.
- A class may need more than one implementation of the method.
##### Use an interface in the following circumstances:
- There is a group of related methods that may be called.
- A class only needs one implementation of the method.
- The class using the interface will want to cast that interface to other interface or class types.
- The method being implemented is linked to the type or identity of the class: for example, comparison methods.

**See example below if the instructions are unclear.**
##### **When to use a Delegate**:
Suppose you have a simple application that calculates the total price of items in a shopping cart. You have a `ShoppingCart` class with a `CalculateTotal` method, and you want to calculate the total price using a delegate. The calling code doesn't need to access any other properties or methods of the `ShoppingCart` class.
```c#
public class ShoppingCart
{
    public decimal CalculateTotal(Func<decimal, decimal> calculateFunction)
    {
        // Simulate adding items to the cart.
        decimal subtotal = 100.0m;
        
        // Calculate the total using the provided delegate.
        decimal total = calculateFunction(subtotal);
        
        return total;
    }
}

class Program
{
    static void Main()
    {
        ShoppingCart cart = new ShoppingCart();

        // Using a delegate to calculate total price.
        Func<decimal, decimal> calculateFunction = subtotal => subtotal * 1.08m; // Apply a tax rate of 8%.

        decimal totalPrice = cart.CalculateTotal(calculateFunction);

        Console.WriteLine("Total Price: " + totalPrice);
    }
}
```
In this example, we use a delegate (`Func<decimal, decimal>`) to calculate the total price, and the calling code doesn't need to access any other properties or methods of the `ShoppingCart` class. Delegate is a single injection.
##### **When to use an Interface**:
Now, let's consider a different scenario where you have a more complex application with multiple operations related to shopping carts. You define an interface to encapsulate these operations, and the calling code may need to access other properties and methods of the `ShoppingCart` class.
```c#
public interface IShoppingCartOperations
{
    decimal CalculateTotal();
    void AddItem(string itemName, decimal price); //itemName and price needs to be accessed 
    void RemoveItem(string itemName);
}

public class ShoppingCart : IShoppingCartOperations
{
    private decimal subtotal = 0.0m;

    public decimal CalculateTotal()
    {
        // Calculate total with tax.
        return subtotal * 1.08m;
    }

    public void AddItem(string itemName, decimal price)
    {
        // Add an item to the cart.
        subtotal += price;
    }

    public void RemoveItem(string itemName)
    {
        // Remove an item from the cart.
        // Implement removal logic.
    }
}

class Program
{
    static void Main()
    {
        ShoppingCart cart = new ShoppingCart();

        // Using an interface to calculate total and interact with other cart operations.
        cart.AddItem("Item 1", 50.0m);
        cart.AddItem("Item 2", 30.0m);

        decimal totalPrice = cart.CalculateTotal();

        Console.WriteLine("Total Price: " + totalPrice);

        // You can also call other methods on the cart if needed.
        cart.RemoveItem("Item 1");
    }
}
```
In this example, we use an interface (`IShoppingCartOperations`) to define a group of related methods for shopping cart operations, and the calling code may need to access other properties and methods of the `ShoppingCart` class beyond just calculating the total. Interface Injects multiple contracts. 

This illustrates the contrast between using delegates for single, specific operations and using interfaces for a broader set of related methods.
