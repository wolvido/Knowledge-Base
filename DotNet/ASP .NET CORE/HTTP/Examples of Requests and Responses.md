Let’s say we have an application that allows you to view, create, edit, and delete customers and orders for a small clothing store hosted at `fashionboutique.com`. We could create an HTTP API that allows a client to perform these functions:

If we wanted to view all customers, the request would look like this:
```
GET http://fashionboutique.com/customers
Accept: application/json
```

A possible response header would look like:
```
Status Code: 200 (OK)
Content-type: application/json
```
followed by the `customers` data requested in `application/json` format.

Create a new customer by posting the data:
```
POST http://fashionboutique.com/customers
Body:
{
  “customer”: {
    “name” = “Scylla Buss”,
    “email” = “scylla.buss@codecademy.org”
  }
}
```

The server then generates an `id` for that object and returns it back to the client, with a header like:
```
201 (CREATED)
Content-type: application/json
```

To view a single customer we _GET_ it by specifying that customer’s id:
```
GET http://fashionboutique.com/customers/123
Accept: application/json
```

A possible response header would look like:
```
Status Code: 200 (OK)
Content-type: application/json
```
followed by the data for the `customer` resource with `id` 23 in `application/json` format.

We can update that customer by _PUT_ ting the new data:
```
PUT http://fashionboutique.com/customers/123
Body:
{
  “customer”: {
    “name” = “Scylla Buss”,
    “email” = “scyllabuss1@codecademy.com”
  }
}
```
A possible response header would have `Status Code: 200 (OK)`, to notify the client that the item with `id` 123 has been modified.

We can also _DELETE_ that customer by specifying its `id`:
```
DELETE http://fashionboutique.com/customers/123
```

The response would have a header containing `Status Code: 204 (NO CONTENT)`, notifying the client that the item with `id` 123 has been deleted, and nothing in the body.