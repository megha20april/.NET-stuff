
- The default server used by ASP.NET Core is Kestrel web server.

# How are requests managed in ASP.NET Core?

- At the start of a request, Kestrel web server receives the HTTP request.
- It passes it to the ASP.NET Core middleware pipeline.
- The framework creates a `HttpContext` instance per request and injects it into the pipeline.
- This context flows through middlewares, controllers, filters, etc.
- Once the response is sent, the context is disposed.

# ❓ What is HttpContext?

`HttpContext` represents all the information about a single HTTP request in an ASP.NET Core web app.

| Property     | Description                                                            |
| ------------ | ---------------------------------------------------------------------- |
| `Request`    | Info about incoming request: headers, cookies, path, query, body, etc. |
| `Response`   | Info about the outgoing response: status code, body, headers, etc.     |
| `User`       | ClaimsPrincipal object that holds authenticated user data.             |
| `Session`    | Server-side session data (if enabled).                                 |
| `Items`      | Per-request storage (key-value).                                       |
| `Connection` | Info about the remote client.                                          |

- It is internally managed, populated and provided by ASP.NET all over its pipeline.
  
