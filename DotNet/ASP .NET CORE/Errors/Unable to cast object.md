---
keywords: Validation error
---
carefull not to add a sting validation to an enum or other data types. 
for example:
```c#
[StringLength(10, ErrorMessage = "Transaction medium cannot exceed 10 characters.")]
public TransactionMedium TransactionMedium { get; set; }
```
This will throw an unable to cast error