Syntax:
![[Capture 7.png]]
HTTP Request is the Start line, Request Headers, and Request body sent to the server from the client as per the method of request e.g. get, post, put, etc. In the get request method the ``Request Body`` is empty, in the post request there would be a `Request Body`. see [[HTTP request methods]].
- the start line syntax is: 
	- The request method eg. get, post, put etc.
	- The URL
	- HTTP version
- Request Headers tells the server what to do with the request, what type of request, or what the client expects from the serve.
- Request body- unlike response body, it does not return html. Depending on the request type may send form data, raw, or url encoded form to the server.

Just like in [[HTTP Response]] has Response headers, HTTP Request has [[HTTP Request Headers]] that tells the server what to do with the request, what type of request, or what the client expects from the serve, just like a [[HTTP Response Headers]] but from client to server.
##### client:
![[Capture 8.png]]
# see this, to know how it works: [[Examples of Requests and Responses]].