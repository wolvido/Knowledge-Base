HTTP is an application-protocol that defines set of rules to send request from browser to server and send response from server to browser. 
see: [[HTTP Response]], [[HTTP Request]]

HTTP stands for "hypertext transfer protocol" - put simply, it's the communication language of the web. For your computer to talk to a web server, they have to both agree on what kinds of things they can talk about, and how the messages will look. So, for example, the web browser knows to send GET when it wants a web page and it knows to send POST when it's sending information. Meanwhile, the web server understands that when a computer says "GET," it should send out the requested information.

HTTP works in a client-server model, where a client (typically a web browser) sends requests for resources like web pages, images, or files to a web server, and the server responds with the requested data. The protocol defines how these requests and responses are formatted and transmitted, making it possible for users to access and interact with websites and web applications.

HTTP is designed to be a stateless protocol, which means that each request from a client to a server is independent and does not carry information about previous requests. This simplicity allows for efficient and scalable web communication. However, for more complex web applications that require maintaining a user's state or session, technologies like cookies and sessions are often used in conjunction with HTTP.
#### What next?
- What is sent from server to client? [[HTTP Response]]
- [[Examples of Requests and Responses]].
- What does 404 or other code means? [[HTTP status codes]]
- What is sent from the client to the server? [[HTTP Request]]
- Post vs get? [[HTTP request methods]]
- These are all good information, so how do I make use of this info? Now you understand how [[HttpClient]] works, and can use it to allow your program to request to api's and or receive responses.
- [[HTTPS]] - Hypertext Transfer Protocol Secure and how to implement it in .NET.