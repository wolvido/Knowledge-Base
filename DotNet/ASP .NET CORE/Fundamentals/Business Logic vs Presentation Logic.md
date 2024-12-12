- Business logic is for the required operations and providing that data to the frontend.
- Presentation logic is the logic concerned in presenting, in how to present, in ways to present, the goal is to present the data provided by the business logic. 
>[!info]
> Its JS that handles the frontend movements and magikens, just remember server-side scripting is to present the data provided by the backend.
### Sample
Let's imagine we have a web application that allows users to place orders for products. We'll focus on the logic involved in calculating the total price of an order.
#### Business Logic:
```c#
// Business Logic (Model or Service Layer)
public class Order
{
    public List<OrderItem> OrderItems { get; set; }

    // Business logic for calculating total price
    public decimal CalculateTotalPrice()
    {
        decimal totalPrice = 0;

        foreach (var orderItem in OrderItems)
        {
            totalPrice += orderItem.Quantity * orderItem.Product.Price;
        }

        return totalPrice;
    }
}

public class OrderItem
{
    public Product Product { get; set; }
    public int Quantity { get; set; }
}

public class Product
{
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```
In this example, the `Order` class contains business logic (`CalculateTotalPrice`) responsible for calculating the total price of an order based on the quantity of each product and its price.
##### Presentation Logic:
```c#
// Presentation Logic (Controller and View)
public class OrderController
{
    // Presentation logic for displaying order details
    public ActionResult DisplayOrderDetails(Order order)
    {
        ViewBag.TotalPrice = order.CalculateTotalPrice(); // Using business logic

        return View(order);
    }
}
```
In the controller, we have presentation logic responsible for preparing data to be displayed in the view. It calls the `CalculateTotalPrice` method from the business logic to determine the total price of the order. The view can then use `ViewBag.TotalPrice` to display this information.
##### View Example (Razor View):
```html
<!-- View (Razor) -->
@model Order

<h2>Order Details</h2>

@foreach (var orderItem in Model.OrderItems)
{
    <p>@orderItem.Quantity x @orderItem.Product.Name - $@orderItem.Product.Price</p>
}

<p>Total Price: $@ViewBag.TotalPrice</p>

```
Conclusion: 
In the view, we use presentation logic to iterate through order items and display relevant information. The total price, calculated by the controller, is then displayed using `ViewBag.TotalPrice`.