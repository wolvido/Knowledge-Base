A cookie is a small amount of data that is persisted across requests and even sessions. Cookies store information about the user. The browser stores the cookies on the user’s computer. Most browsers store the cookies as key-value pairs.
- At first, server sends a cookie (key/value pair) by using a response header called “Set-Cookie”. Then the browser receives it and stores the cookie in the browser memory.
- For each subsequent request, the same cookie will be sent to the server with “Cookie” request header.
###### **To write a cookie in ASP.NET Core:**
`Response.Cookies.Append(key, value);`