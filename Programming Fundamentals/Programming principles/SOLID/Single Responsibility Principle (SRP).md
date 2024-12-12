- This principle states that a class should have only one reason to change, meaning that the only thing you need to rewrite is the how of the class not the why.
- It encourages the separation of concerns by ensuring that each class or module is responsible for a single, well-defined task.
- A class that can be rewritten for a different purpose will destroy everything that depends on it.

Martin defines a responsibility as a _reason to change_, and concludes that a class or module should have one, and only one reason to be changed/rewritten. 

Sample:
```c#
public class Invoice
{
            public void AddInvoice()
            { 
                // your logic
            }

            public void DeleteInvoice()
            { 
                // your logic
            }

            public void GenerateReport()
            { 
                // your logic
            }

            public void EmailReport()
            { 
                // your logic
            }
}
```
Invoice class seems to handle Invoicing and more, geeks for geeks suggest:
![[Pasted image 20231010160219.png]]

```c#
public class Invoice
{
            public void AddInvoice()
            {
                // your logic
            }

            public void DeleteInvoice()
            {
                // your logic
            }
}

public class Report
{

            public void GenerateReport()
            {
                // your logic
            }
}

public class Email
{
            public void EmailReport()
            {
                // your logic
            }
}
```

It also might depend on the design pattern, for resource centric design, the encapsulation will depend on the resource.
- Like for example the Employee resource, you make a **`EmployeeService.cs`**, the employee service will have the all the crud methods, and all the additional necessary methods for whatever the site needs employee related. Like for example it will have a SortBy method for the list of employee display.
###### Remember It is a guideline, use it as such. The main point is to create a class with a single reasonable responsibility.