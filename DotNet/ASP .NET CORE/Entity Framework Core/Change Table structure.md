Once you've already created a table structure in your DB, how do you change or update it?
for example in the persons model:
```c#
public class Person
{
    [Key] //means main key
    public int PersonId { get; set; }
    [StringLength(40)]
    public string? Name { get; set; }
    [StringLength(40)]
    public string? Email { get; set; }
    [StringLength(10)] //you can set gender to 10
    public string? Gender { get; set; }
}
```
We have already run the command `Update-Database`.
###### Lets say we want to add the property:
```c#
[StringLength(200)]
public string? Address {get; set;}
```
Simply use the same migration system used here [[Code-First Migrations]].
- Run: `Add-Migration AddressColumn`.
- Then Run: `Update-Database`.
>[!warning]
>If you already have rows with existing data, then the the new column is going to be null on the existing rows.
>IF Needed, Run an sql command on the Up of the migration that adds data.
#### IF you want to remove a property
Simply remove it from the model and do the same process.
