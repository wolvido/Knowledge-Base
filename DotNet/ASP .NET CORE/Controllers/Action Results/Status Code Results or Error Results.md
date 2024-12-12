---
keywords: |-
  how to return error in MVC
  How to error in MVC
---
Action Results for status codes.
see [[HTTP status codes]] for more info
##### BadRequestResult
```c#
return BadRequest("Book ID is empty");
```
will return a status code 400 Bad Request, and an error body content message that is optional. Used when the request values are invalid(validation error).

If you used and object as parameter to bad request, it will serialize it into a json response:
```c#
var errorResponse = new ErrorResponse
{
    ErrorCode = "400",
    ErrorMessage = "Validation Failed",
    Details = new List<string> { "Name is required", "Age must be a positive number" }
};

return BadRequest(errorResponse);
```
will return:
```json
{
    "errorCode": "400",
    "errorMessage": "Validation Failed",
    "details": [
        "Name is required",
        "Age must be a positive number"
    ]
}
```
##### NotFoundResult
```c#
return NotFound("Book not found");
```
returns a 404 not found, optional body content.  Used when request is not available at server.
Can also accept object and serialize it into JSON, just like `BadRequestResult`.
##### UnauthorizedResult
```c#
return Unauthorized("Access not authorized");
```
returns a 401 Unauthorized. Used when unauthorized.
##### StatusCodeResult
```c#
return StatusCode(statusCode, "optional body content");
```
Manually set the status code to any code.
see [[HTTP status codes]] for more info