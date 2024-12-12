# This is what I understand so far:
- REST is REST (Representational State Transfer), REST defines a set of guidelines for designing web services to be more scalable, flexible, and easy to develop. It is not limited to API's.
- When making an API, you usually use REST architecture, that's why it's called RESTfull API.
- RESTful APIs are the de-facto standard for modern web service APIs.
- Every modern web development frameworks and technologies provide built-in tools or libraries for RESTful APIs.
- So essentially, RESTful is what we are already using right now, already implemented in the tech, everything here [[HTTP]] is RESTful.
##### Statelessness
Server does not need to know anything about what state the client is in and vice versa. Each request from a client to a server must contain all the information necessary for the server to fulfill that request. Each request from a client to a server must contain all the information required by the server to understand and process the request.
- Wait but what about user accounts, isn't that info on the client? what is "state" exactly?
Each request must contain all the necessary information for the server to process it, including any authentication tokens or identifiers needed to associate the request with a specific user account.
The server can still store user accounts as entities and the client can use and modify the user accounts, but ==the server does not need "remember anything" in order to interact with the client==. That's what statelessness is.
#### Requests
REST requires that a client make a request to the server in order to retrieve or modify data on the server. A request generally consists of:
- an HTTP verb or [[HTTP request methods]], which defines what kind of operation to perform. 
- a _header_ or [[HTTP Response Headers]], which allows the client to pass along information about the request.
- a path to a resource, aka a link `/website/account/etc.`.
- an optional message body containing data.
#### Response
Response is the server responding to a request. see [[HTTP Response]].
#### see: [[Examples of Requests and Responses]]
