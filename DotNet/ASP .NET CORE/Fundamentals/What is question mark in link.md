---
keywords: what is ? in link
---
It's a query string. A query string is a way to pass data to a web server when making an HTTP request, typically via a GET request. The query string contains key-value pairs

```http
http://example.com/path/resource?param1=value1&param2=value2
```
In the above example, the "?" marks the start of the query string, and the key-value pairs are separated by "&" characters. For instance, `param1=value1` and `param2=value2` are parameters and their corresponding values.

Web servers can use the data in the query string to customize the response or perform specific actions based on the provided parameters. Web applications often use query strings to pass information between web pages, search for specific content, or customize the behavior of a webpage.

You can also add two or more key value pair separating them using ampersand "&."
```http
http://example.com/path/resource?param1=value1&param2=value2&param3=value3
```

