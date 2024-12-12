1. High-level modules should not import anything from low-level modules. Both should depend on abstractions (e.g., interfaces).
2. Abstractions should not depend on details (concrete implementations). Details should depend on abstractions.

- High level modules (The one using other classes or methods; the top of the dependency pyramid)
- Low level modules (The one being used by High level modules; the bottom of the dependency pyramid)
- Abstraction (Interface or delegates)

Rule 2 means the high level module should depend on the abstraction(interface), rather than implement their own low level modules.

So basically just the way you naturally use interface or delegates.

Sample:
```c#
public interface INotificationSender // This is the Abstraction
{
    void Send(string message);
}

public class EmailSender : INotificationSender // Concrete implementation for sending emails this is the low level
{
    public void Send(string message)
    {
        Console.WriteLine($"Sending an email: {message}");
    }
}

public class SMSSender : INotificationSender // another low level
{
    public void Send(string message)
    {
        Console.WriteLine($"Sending an SMS: {message}");
    }
}

public class NotificationService // High-level module that depends on INotificationSender (abstraction)
{
    private readonly INotificationSender _sender;

    public NotificationService(INotificationSender sender)
    {
        _sender = sender;
    }

    public void SendNotification(string message)
    {
        _sender.Send(message);
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Using the NotificationService with different senders
        var emailSender = new EmailSender();
        var smsSender = new SMSSender();
        
        var emailNotify = new NotificationService(emailSender);
        var smsNotify = new NotificationService(smsSender);
        
        emailNotify.SendNotification("Hello, this is an email!");
        smsNotify.SendNotification("Hello, this is an SMS!");
        
    }
}
```
The advantage is very low coupling and extensibility. 
If you directly implement ``EmailSender`` and ``SMSSender`` to ``NotificationService`` then if you need a different sender algorithm you will have to modify ``NotificationService`` every time compared to just injecting. see [[Interface Extensibility and Polymorphism]] for more info.

If you implemented it like this:
```c#
// High-level module that directly depends on concrete implementations
public class NotificationService
{
    private readonly EmailSender emailSender;
    private readonly SMSSender smsSender;
    //youre gonna have to edit it for every new algorithm like:
    //private readonly AppSender appSender;
    //instead of using an abstraction that would make it more extensible as long as the sender contract is fulfilled

    public NotificationService()
    {
        this.emailSender = new EmailSender();
        this.smsSender = new SMSSender();
    }

    public void SendEmailNotification(string message)
    {
        emailSender.SendEmail(message);
    }

    public void SendSMSNotification(string message)
    {
        smsSender.SendSMS(message);
    }
}
```
###### Also see [[Dependency Injection]].




