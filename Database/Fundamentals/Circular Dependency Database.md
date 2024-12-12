Circular Dependency is considered bad practice.

The problem with circular dependencies is like the chicken and egg problem.
If you depend on me setting something up, and I depend on you setting something up, how do we start?
Also how do we end? If I have a reference to your resource and you have a reference to mine, I can never clean up because that would break you, and you cannot clean up because that would break me.

The answer in both cases is to introduce a middleman, passing the dependency from one of the parties to him, So if you passed your resource on to the middleman, you would depend on me and the middleman, and I would depend on the middleman. Thus you can clean up because you now hold no resource, and I can clean up because no-one depends on me, and then the middleman can clean up.

https://stackoverflow.com/a/11577631/13107848

Consider cities and states. Each city exists within a state. Each state has a capital city.
```sql
CREATE TABLE city (
  city  VARCHAR(32),
  state VARCHAR(32) NOT NULL,
  PRIMARY KEY (city),
  FOREIGN KEY (state) REFERENCES state (state)
);

CREATE TABLE state (
  state VARCHAR(32),
  capital_city VARCHAR(32),
  PRIMARY KEY (state),
  FOREIGN KEY (capital_city) REFERENCES city (city)
);
```
First problem - You cannot create these tables as shown, because a foreign key can't reference a column in a table that doesn't (yet) exist.
Second problem - you cannot insert rows into either table, as each insert will require a pre-existing row in the other table.

Workarounds exist in these problems but there are better ways to design as to not have a circular dependency. Mainly by creating middlemen. 
#### Sample problem:
###### There are two tables: 
- User 
- Address 
User contains a reference to Address. Address contains the columns CreatedBy and ModifiedBy, which is reference to User creating a cyclic dependency. How to design this database to avoid a cyclic dependency?
###### Introduce middleman table to manage the relationship
```json
// User table
User {
    UserId: INT PRIMARY KEY,
    UserName: VARCHAR(255),
    // Other user-related columns
}

// Address table
Address {
    AddressId: INT PRIMARY KEY,
    Street: VARCHAR(255),
    City: VARCHAR(255),
    // Other address-related columns
}

// UserAddress table (Linking table)
UserAddress {
    UserId: INT,
    AddressId: INT,
    CreatedBy: INT,
    ModifiedBy: INT,
    PRIMARY KEY (UserId, AddressId),
    FOREIGN KEY (UserId) REFERENCES User(UserId),
    FOREIGN KEY (AddressId) REFERENCES Address(AddressId),
    FOREIGN KEY (CreatedBy) REFERENCES User(UserId),
    FOREIGN KEY (ModifiedBy) REFERENCES User(UserId)
}
```
- `User` and `Address` are independent tables without direct references to each other.
- `UserAddress` serves as a linking table to establish the relationship between users and addresses.
- `UserAddress` includes foreign keys pointing to both `User` and `Address`, as well as `CreatedBy` and `ModifiedBy` columns indicating the users who created and modified the relationship.

This design allows each user to have an associated address and maintains the necessary references without creating a direct cyclic dependency between the `User` and `Address` tables.