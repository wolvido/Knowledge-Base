---
keywords: |-
  What does http status codes mean
  what does 404 mean
---
![[Capture 4.png]]
**1xx Informational:**
- 100 Continue: The server has received the initial part of the request, and the client should proceed with the rest of the request.

**2xx Success:**
- 200 OK: The request was successful, and the server has provided the requested resource.
- 201 Created: The request was successful, and the server has created a new resource as a result.
- 204 No Content: The request was successful, but there is no data to return in the response body.

**3xx Redirection:**
- 301 Moved Permanently: The resource has been permanently moved to a different URL, and the client should update its bookmarks.
- 302 Found (or 303 See Other): The resource is temporarily located at a different URL. The client should continue to use the original URL for future requests.
- 307 Temporary Redirect: Similar to 302, indicating a temporary redirection.

**4xx Client Errors:**
- 400 Bad Request: The request is invalid or malformed.
- 401 Unauthorized: Authentication is required, and the client failed to provide valid credentials.
- 403 Forbidden: The client does not have permission to access the requested resource.
- 404 Not Found: The requested resource could not be found on the server.
- 405 Method Not Allowed: indicates that the server knows the request method, but the target resource doesn't support this method

**5xx Server Errors:**
- 500 Internal Server Error: A generic error message indicating a problem with the server.
- 501 Not Implemented: The server does not support the functionality needed to fulfill the request.
- 502 Bad Gateway: The server acting as a gateway or proxy received an invalid response from an upstream server.
- 503 Service Unavailable: The server is temporarily unable to handle the request due to overload or maintenance.
- 504 Gateway Timeout: server acting as a gateway or proxy, did not receive a timely response from an upstream or origin server it needed to access in order to complete the request.

also see: [[How to manually assign a status code in a middleware]]