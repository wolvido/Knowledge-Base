All examples will be based on this simple data model:

> A `Person` entity has five properties: `Id, FirstName, LastName, Age, CityId`

And you can assume that the application uses this data in many varied ways (reports, forms, popups, ...).

The entire application already exists. Everything I mention is a change to the existing codebase. This is important to remember.

---

**Example 1 - Changing the underlying data structure - Without DTO**

The requirements have changed. The age of the person needs to be dynamically retrieved from the government's database (let's assume based on their first and last name).

Since you don't need to store the `Age` value locally anymore, it therefore needs to be removed from the `Person` entity. It's important here to realize that the entity represents **the database data**, and nothing more. If it's not in the database, it's not in the entity.  
When you retrieve the age from the government's web service, that will be stored in a different object (or int).

But your frontend still displays an age. All the views have been set up to use the `Person.Age` property, which now no longer exists. A problem presents itself: **All views that refer to the `Age` of a person need to be fixed**.

---

**Example 2 - Changing the underlying data structure - With DTO**

In the old system, there is also `PersonDTO` entity with the same five properties: `Id, FirstName, LastName, Age, CityId`. After retrieving a `Person`, the service layer converts it to a `PersonDTO` and then returns it.

But now, the requirements have changed. The age of the person needs to be dynamically retrieved from the government's database (let's assume based on their first and last name).

Since you don't need to store the `Age` value locally anymore, it therefore needs to be removed from the `Person` entity. It's important here to realize that the entity represents **the database data**, and nothing more. If it's not in the database, it's not in the entity.

However, since you have an intermediary `PersonDTO`, it's important to see that this class can **keep** the `Age` property. The service layer will fetch the `Person`, convert it to a `PersonDTO`, it will then also fetch the person's age from the government's web service, will store that value in `PersonDTO.Age`, and passes that object.

The important part here is that **anyone who uses the service layer doesn't see a difference between the old and the new system**. This includes your frontend. In the old system, it received a full `PersonDTO` object. And in the new system, it still receives a full `PersonDTO` object. **The views do not need to be updated**.

This is what we mean when we use the phrase **separation of concerns**: There are two different concerns (storing the data in the database, presenting data to the frontend) and they need a different data type each. Even if those two data types happen to contain the same data right now, that might change in the future.  
In the given example, `Age` is a difference between the two data types: `Person` (the database entity) doesn't need an `Age`, but `PersonDTO` (the frontend data type) does need it.  
By separating the concerns (= creating separate data types) from the beginning, the codebase is much more resilient to changes made to the data model.

> You might argue that having a DTO object, when a new column is added to the database, means you have to do double work, adding the property in both the entity and the DTO. That is _technically_ correct. It requires a bit of extra effort to maintain two classes instead of one.
> 
> However, you need to compare the effort required. When one or more new columns are added, copy/pasting a few properties doesn't take all that long. When the data model changes structurally, having to change the frontend, possibly in ways that only cause bugs at runtime (and not at compile time), takes considerably more effort, and it requires the developer(s) to go hunting for bugs.

---

I could give you more examples but the principle will always be the same.

**To summarize**

- Separate responsibilities (concerns) need to work separately from each other. They should not share any resources such as data classes (e.g. `Person`)
- Just because an entity and its DTO have the same properties, does not mean that you need to merge them into the same entity. Don't cut corners.
    - As a more blatant example, let's say our database contains countries, songs and people. All of these entities have a `Name`. But just because they all have a `Name` property, doesn't mean that we should make them inherit from a shared `EntityWithName` base class. The different `Name` properties have no meaningful relation.
    - Should one of the properties ever change (e.g. a song's `Name` gets renamed to `Title`, or a person gets a `FirstName` and `LastName`), they you'll have to spend more effort undoing the inheritance _which you didn't even need in the first place_.
    - Although not as blatant, your argument that you don't need a DTO when you have an entity is the same. You're looking at the _now_, but you're not preparing for any future changes. **IF** the entity and DTO are exactly the same, and **IF** you can guarantee that there will never be any changes to the data model; then you are correct that you can omit the DTO. But the thing is that you can never guarantee that the data model will never change.
- Good practice doesn't always pay off immediately. It might start paying off in the future, when you need to revisit an old application.
- The main killer of existing codebases is letting the code quality drop, continually making it more difficult to maintain the codebase, until it devolves into a useless mess of spaghetti code that's unmaintainable.
- Good practice, such as implementing a separation of concerns from the get to, aim to avoid that slippery slope of bad maintenance, in order to keep the codebase maintainable for as long as possible.

---

As a rule of thumb to consider separating concerns, think of it this way:

Suppose that every concerns (the UI, the database, the logic) is handled by a different person in a different location. They can only communicate by email.

In a well-separated codebase, a change to a particular concern will only need to be handled by one person:

- Changing the user interface only involves the UI dev.
- Changing the data storage method only involves the database dev.
- Changing the business logic only involves the business dev.

If all of these developers were using the same `Person` entity, and a minor change was made to the entity, **everyone** would need to be involved in the process.

But by using separate data classes for every layer, that issue isn't as prevalent:

- As long as the database dev can return a valid `PersonDTO` object, the business and UI dev do not care that he changed how the data is stored/retrieved.
- As long as the business dev stores the data in the database, and provides the needed data to the frontend, the database and UI devs don't care if he decided to rework his business rules.
- As long as the UI can be designed based around the `PersonViewModel, then the UI dev can built the UI however they want. The database and business devs don't care how it is done, since it doesn't affect them.

The key phrase here is **since it doesn't affect them**. Implementing a good separation of concerns seeks to minimize affecting (and therefore having to involve) other parties.

_Of course, some major changes can't avoid including more than one person, e.g. when an entirely new entity is added to the database. But don't underestimate the amount of minor changes that you have to make during an application's lifetime. Major changes are a numerical minority._
___
#### What if we map DTO's exactly as the Entities and NOT base it on use-case?
Aside from the reasons explained above,  you're code will just... make no sense. 
Sure it will add a layer of separation but it would make very little sense, If you decide to change the entities, then the DTO would just be an older version of your entities, keep this up and you'll end up with a DTO that is completely outdated an makes no sense and needs to be updated. Now if a DTO needs to be "updated", then that completely defeats the purpose of a DTO, an updated DTO would ruin frontend code and you would need to hunt and rewrite a lot of shite.
If you make DTO's based on use-case, then no matter how you change your entities your DTO's wont need unnecessary "updates" and they would actually serve their purpose.