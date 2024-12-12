#cSharp 
- **Join**: Performs an inner join between two sequences.
- **GroupJoin**: Performs a group join between two sequences.
- **Zip**: Merges two sequences element-wise.
```c#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

class Order
{
    public int OrderId { get; set; }
    public string Product { get; set; }
}

List<Order> orders = new List<Order>
{
    new Order { OrderId = 1, Product = "Product A" },
    new Order { OrderId = 2, Product = "Product B" },
    new Order { OrderId = 3, Product = "Product C" },
};

class OrderDetail
{
    public int OrderId { get; set; }
    public decimal Price { get; set; }
}

List<OrderDetail> orderDetails = new List<OrderDetail>
{
    new OrderDetail { OrderId = 1, Price = 10.99M },
    new OrderDetail { OrderId = 2, Price = 25.49M },
    new OrderDetail { OrderId = 4, Price = 5.99M },
};

// Join: Performs an inner join between two sequences
var innerJoin = orders.Join(orderDetails,
    order => order.OrderId,
    detail => detail.OrderId,
    (order, detail) => new
    {
        OrderId = order.OrderId,
        Product = order.Product,
        Price = detail.Price
    });

Console.WriteLine("Inner Join (Orders and OrderDetails):");
foreach (var item in innerJoin)
{
    Console.WriteLine($"Order ID: {item.OrderId}, Product: {item.Product}, Price: {item.Price:C}");
}

// GroupJoin: Performs a group join between two sequences
var groupJoin = orders.GroupJoin(orderDetails,
    order => order.OrderId,
    detail => detail.OrderId,
    (order, details) => new
    {
        OrderId = order.OrderId,
        Product = order.Product,
        Prices = details.Select(detail => detail.Price)
    });

Console.WriteLine("Group Join (Orders and OrderDetails):");
foreach (var item in groupJoin)
{
    Console.WriteLine($"Order ID: {item.OrderId}, Product: {item.Product}");
    foreach (var price in item.Prices)
    {
        Console.WriteLine($"Price: {price:C}");
    }
}

// Zip: Merges two sequences element-wise
var zipped = orders.Zip(orderDetails,
    (order, detail) => new
    {
        OrderId = order.OrderId,
        Product = order.Product,
        Price = detail.Price
    });

Console.WriteLine("Zip (Orders and OrderDetails):");
foreach (var item in zipped)
{
    Console.WriteLine($"Order ID: {item.OrderId}, Product: {item.Product}, Price: {item.Price:C}");
}
```