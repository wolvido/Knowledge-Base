ISP suggests that clients should not be forced to depend on interfaces they do not use. 
In other words, a class should not be forced to implement interface contracts that it does not need.
> Clients are the class that uses the interface.

The main point is to avoid merging in an interface operations that are not always relevant and required and that leads to dependency hell. In essence this is about separation of concerns.
###### Sample:
```c#
// This is not ISP way of implementing an interface
public interface IMessageSender {
    void SendEmail(string to, string subject, string body);
    void SendSms(string phoneNumber, string message);
    void SendPushNotification(string deviceId, string message);
}
```
The problem with the sample above is, is the grouping of these methods relevant to anything? who needs an `IMessageSender`? is it relevant to anything?

What if no client uses an `IMessageSender`?
What if a there is only a client that needs to send an email only or an SMS only, your client will be forced to implement a `SendSms` and a `SendPushNotification` just so it can have a `SendEmail`. That kind of design will eventually lead to dependency hell.
###### It might be better to implement them separately:
```c#
// Interface for sending email messages
public interface IEmailSender {
    void SendEmail(string to, string subject, string body);
}

// Interface for sending SMS messages
public interface ISmsSender {
    void SendSms(string phoneNumber, string message);
}

// Interface for sending push notifications
public interface IPushNotificationSender {
    void SendPushNotification(string deviceId, string message);
}
```
###### So that the client that only needs an Email Sender will not need to use other dependencies:
```c#
public class EmailService : IEmailSender {
    public void SendEmail(string to, string subject, string body) {
        // Implementation to send email
    }
}
```

	A good analogy for the ISP principle would be: 
You do not want to make a coffee machine need to implement how to print a paper, and a printer to implement how to make coffee, but a coffee machine making different coffees is in its scope.
#### Questions
###### **Doesn't this mean ultimately mean that interfaces should only have one method each?**
The main purpose of the [Interface Segregation Principle](https://en.wikipedia.org/wiki/Interface_segregation_principle) is not to multiply interfaces by unnecessarily segregating them; it's about avoiding to merge in an interface operations that are not always relevant and required. In other words, it's about meaningful separation of concerns.
###### **Isn't this exactly the same as [[Single Responsibility Principle (SRP)]] but applied to interfaces?**
Yes but much more, they are essentially a requirement for each other. 
SRP only says that the class should have only one reason to change, and sometimes when changing that class, you might add some extra "weight" as long as the reason to change is the same. ISP focuses on that and makes sure that by changing the class, you are making sure that the class does not add extra "weight" and becomes too "heavy".
###### Remember It is a guideline, use it as such. The main point is to avoid merging in an interface operations that are not always relevant and required. In other words, it's about meaningfull separation of concerns.
