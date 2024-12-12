#cSharp 
Why using interface is better at unit testing.
Suppose you have a `PaymentProcessor` class responsible for processing payments. This class depends on external services for payment processing, and it directly creates instances of these services. 
```c#
public class PaymentProcessor
{
    private PaymentGateway _paymentGateway;

    public PaymentProcessor()
    {
        // The class creates an instance of the PaymentGateway internally.
        _paymentGateway = new PaymentGateway();
    }

    public bool ProcessPayment(decimal amount)
    {
        // Actual payment processing logic using the payment gateway.
        // ...
        // Calls to _paymentGateway.ProcessPayment() here.
        // ...
        return true; // Simplified result for demonstration.
    }
}
```
In this example:

1. The `PaymentProcessor` class tightly depends on the `PaymentGateway` class, as it directly creates an instance of it in its constructor.
2. The `ProcessPayment` method of `PaymentProcessor` uses the concrete `paymentGateway` instance for processing payments.

Now, let's say you want to unit test the `ProcessPayment` method in isolation without actually making real payment calls. Because of the tight coupling to the concrete `PaymentGateway`, it's difficult to achieve isolation. Here's why:
```c#
[Test]
public void TestProcessPayment()
{
    // Arrange
    var paymentProcessor = new PaymentProcessor();

    // Act
    bool result = paymentProcessor.ProcessPayment(100.0m);

    // Assert
    // It's challenging to isolate and test the ProcessPayment method
    // without actually invoking real payment processing.
    // You can't easily substitute a mock PaymentGateway.
}
```
In this test scenario, it's challenging to isolate `PaymentProcessor` because it creates the `PaymentGateway` internally, and there's no easy way to substitute a mock or stub `PaymentGateway` for testing. This tight coupling makes it difficult to unit test the `ProcessPayment` method in isolation.

To address this issue, you would typically refactor the `PaymentProcessor` class to use dependency injection and depend on an interface for the payment gateway. This way, during testing, you can provide a mock or stub implementation of the payment gateway to isolate the `PaymentProcessor` for unit testing.