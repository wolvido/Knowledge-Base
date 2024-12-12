Using the built in exceptions might not be so useful for large applications with tons of methods, it might be better to create custom exceptions to specify the real exception.

You can create custom exceptions by defining a new class that derives from the `Exception` base class take the base constructor and derive from it:
```c#
public class CustomException : Exception
{
	public MyCustomException()
	{ } 
	
	public MyCustomException(string message) 
		: base(message) { }
		
	public CustomException (string message, Exception innerException)
		: base (message, innerException)
	
	public CustomException (type1 arg,  type2 arg2) //optional custom constructor if necessary
	{
		//...
	}
		
	// You can add custom properties or methods to your exception class
	public string AdditionalInformation { get; set; }
}
```
 Notice we added the parameter less constructor, a constructor that takes a string message, and a constructor that takes a string message and an inner exception and all derived from the base. Adding these three common constructors is convention according to MSDN see [Best Practices for exceptions - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/standard/exceptions/best-practices-for-exceptions?redirectedfrom=MSDN#include-three-constructors-in-custom-exception-classes)
 - You can add more overloads as necessary.
 - And you can also inherit from all the other built-in exception.
>[!warning] Important
>in a .NET project, you need to create a separate class library to store your exceptions; name the library as "Exceptions".

sample of a custom exception:
```c#
using System;

public class InsufficientBalanceException : Exception
{
    public decimal CurrentBalance { get; }
    public decimal WithdrawalAmount { get; }

    public InsufficientBalanceException()
    {
    }

    public InsufficientBalanceException(string message)
        : base(message)
    {
    }

    public InsufficientBalanceException(string message, Exception innerException)
        : base(message, innerException)
    {
    }

	//custom constructor
    public InsufficientBalanceException(decimal currentBalance, decimal withdrawalAmount) 
    {
        CurrentBalance = currentBalance;
        WithdrawalAmount = withdrawalAmount;
    }

    public override string Message //custom message
    {
        get
        {
            return $"Withdrawal amount of {WithdrawalAmount:C} exceeds current balance of {CurrentBalance:C}.";
        }
    }
}

public class BankAccount
{
    private decimal _balance;

    public decimal Balance => _balance;

    public BankAccount(decimal initialBalance)
    {
        _balance = initialBalance;
    }

    public void Withdraw(decimal amount)
    {
        if (amount > _balance)
        {
            throw new InsufficientBalanceException(_balance, amount);
        }

        _balance -= amount;
        Console.WriteLine($"Withdrawal of {amount:C} successful. Remaining balance: {_balance:C}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        BankAccount account = new BankAccount(1000);

        try
        {
            account.Withdraw(1500);
        }
        catch (InsufficientBalanceException ex)
        {
            Console.WriteLine("Insufficient balance error:");
            Console.WriteLine(ex.Message);
            Console.WriteLine($"Current balance: {ex.CurrentBalance:C}");
            Console.WriteLine($"Attempted withdrawal: {ex.WithdrawalAmount:C}");
        }
        catch (Exception ex)
        {
            Console.WriteLine("An unexpected error occurred:");
            Console.WriteLine(ex.Message);
        }
    }
}

```
It is more meaningful than low level un-intelligible stack trace and error message.
