Table Relations in Entity Framework Core. Primary Key, foreign key connections and all that.
# How it works?
A relational Database has 3 main types of relationship:
- one-to-one
- one-to-many
- many-to-many
Sample:
![[Pasted image 20240201151853.png]]
So How do we implement this in EF Core?
##### Relationships
First you have to understand how Relational Entities work in EF Core. It is the same as the DB sample above, essentially the parent model will have a second ID property, the second one will be a foreign ID from a child model. Essentially equivalent to a foreign key in a database.
EF Core relationships is all about mapping the foreign key representation used in a relational database to the references between objects used in an object model.
**In the most basic sense, this involves:**
- Adding a primary key property to each entity type/model.
- Adding a foreign key property to one entity type/model.
- Associating the references between entity types with the primary and foreign keys to form a single relationship configuration.
##### Example of a one-to-one relationship:
```c#
public class Blog // Principal (parent)
{
    public int Id { get; set; }
    public BlogHeader? Header { get; set; } // Reference navigation to dependent
}

public class BlogHeader // Dependent (child)
{
    public int Id { get; set; }
    public int BlogId { get; set; } // Foreign key property - REQUIRED type
    public Blog Blog { get; set; } = null!; // Reference navigation to principal - REQUIRED type
}
```
Means a Blog Header has one Blog and vice versa.
**Remember: The child is the one with the foreign key.**
>[!question] Why the child has the foreign key? why is there a parent child relationship in the first place? Why cant they be both connected to each other?
>They can be connected to each other but that is bad design, there needs to be a dependency hierarchy. see: [[Circular Dependency Database]] for more info.
###### Optional One-to-One:
```c#
// Principal (parent)
public class Blog
{
    public int Id { get; set; }
    public BlogHeader? Header { get; set; } // Reference navigation to dependent
}

// Dependent (child)
public class BlogHeader
{
    public int Id { get; set; }
    public int? BlogId { get; set; } // Optional foreign key property
    public Blog? Blog { get; set; } // Optional reference navigation to principal
}
```
- Same as the previous example, except that the foreign key property and navigation to the principal are nullable, which means the relationship is optional and the child can either have a parent or independent.
##### Example of one-to-many:
```c#
public class Blog // Principal (parent)
{
    public int Id { get; set; }
    public ICollection<Post> Posts { get; } = new List<Post>(); // Collection navigation containing dependents
}

public class Post // Dependent (child)
{
    public int Id { get; set; }
    public int BlogId { get; set; } // Foreign key property - REQUIRED type
    public Blog Blog { get; set; } = null!; // Reference navigation to principal - REQUIRED type
}
```
- Means one post has one blog and one blog has many posts.
###### Optional one-to-many:
```c#
// Principal (parent)
public class Blog
{
    public int Id { get; set; }
    public ICollection<Post> Posts { get; } = new List<Post>(); // Collection navigation containing dependents
}

// Dependent (child)
public class Post
{
    public int Id { get; set; }
    public int? BlogId { get; set; } // Optional foreign key property
    public Blog? Blog { get; set; } // Optional reference navigation to principal
}
```
##### Many-to-many basic sample:
```c#
public class Post
{
    public int Id { get; set; }
    public ICollection<Tag> Tags { get; } = [];
}

public class Tag
{
    public int Id { get; set; }
    public ICollection<Post> Posts { get; } = [];
}
```
see: [Many-to-many relationships - EF Core | Microsoft Learn](https://learn.microsoft.com/en-us/ef/core/modeling/relationships/many-to-many) for more complex samples.

#### How EF Core Navigates?
###### - How Does EF core know that **`public int BlogId { get; set; }`** is a foreign key and not just a regular property?
EF uses convention, it makes a property as a foreign key property when its name matches with the primary key property of a related entity.  see: [Conventions for relationship discovery - EF Core | Microsoft Learn](https://learn.microsoft.com/en-us/ef/core/modeling/relationships/conventions#reference-navigations) for more details.
###### - Wait what about the many-to-many sample? there is no Id property there
Essentially, it checks whether the property is an `IEnumerable<TEntity>`, in this case it is `ICollection<Tag>` and `ICollection<Post>` see: [Conventions for relationship discovery - EF Core | Microsoft Learn](https://learn.microsoft.com/en-us/ef/core/modeling/relationships/conventions#collection-navigations) for more info
###### - What if I don't want to follow convention, what if I want something like `BlogForeignKey` instead?
Aside from the default convention, you can also specify by using `[ForeignKey("NameOfEntity")]` attribute. sample:
```c#
// Dependent (child)
public class BlogHeader
{
    public int Id { get; set; }
    
    [ForeignKey("Blog")]
    public int? BlogForeignKey { get; set; } // Foreign key property
    public Blog? Blog { get; set; } // Reference navigation to principal
}
```
#### So, how do I make use of this?
Well first, you will not be able to make use of it in LINQ without including it, To include it, you use Fluent API's **`Include()`**.
###### How-to?
For example, if we use this model:
```c#
public class Blog // Principal (parent)
{
    public int Id { get; set; }
    public BlogHeader? Header { get; set; } // Reference navigation to dependent
}

public class BlogHeader // Dependent (child)
{
    public int Id { get; set; }
    public int? BlogId { get; set; } // Foreign key property
    public Blog? Blog { get; set; } // Reference navigation to principal
}
```
###### In your service, the service that calls the data for the model, for example:
```c#
public List<BlogHeader> GetAllBlogHeader()
{
	return _db.BlogHeaders.ToList();
}
```
This returns a list of **`BlogHeaders`** from the database, but it will return the **`Blog`** as null.
###### In order to include its relationship with **`Blog`**, we need to add `Include()`:
```c#
public List<BlogHeader> GetAllBlogHeader()
{
	return _db.BlogHeaders.Include("Blog").ToList();
}
```
- The syntax is `Include("NameOfTheForeignProperty")`.
>[!warning] Remember
>It's not the model/entity name, it is the property name inside the model. It's called the navigation property.
# There is also a way in Fluent API to establish the relationships
You can look it up, normally you wouldn't need to use it.