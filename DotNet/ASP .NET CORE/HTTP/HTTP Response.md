**syntax:**
![[github guide.png]]
###### HTTP Response is the response from a client request sent by the server.
A Response contains:
- The **start line** indicates the HTTP version, the status code, and the description, see [[HTTP status codes]] for more info.
- **Response headers** are the key value pairs that are sent by the server to the client, generally it tells the client what to do with the response, what type of response, or the response itself. see [[HTTP Response Headers]]
- **Response body** is the html itself, the page itself, the one the user uses.
sample:
![[Capture 2.png]]
response headers can be more, not just date or content-type, see sample below.

sample of the response headers on edge:
![[Capture 1.png]]
for detailed info see: [[HTTP Response Headers]]


**Syntax of the response start line:**
![[Capture 3.png]]
To know what the status codes mean see: [[HTTP status codes]]
# see this, to know how it works: [[Examples of Requests and Responses]].