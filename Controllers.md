
## Controller Base Classes

Controllers in ASP.NET Core inherit from one of these base classes:

1. Controller Class (Most Common)
   
```csharp
public class UsersController : Controller
{
    // Your actions here
}
```
The Controller class provides:

- View rendering capabilities (View(), PartialView())
- Redirect methods (RedirectToAction(), Redirect())
- HTTP response helpers (Ok(), NotFound(), BadRequest())
- Access to HttpContext, Request, Response objects
- Model binding and validation features
- TempData for temporary storage between requests

2. ControllerBase Class (For APIs)
   
```csharp
public class ApiController : ControllerBase
{
    // API actions here
}
```
ControllerBase is lighter - it excludes view-relateedd fnctionality since APIs don't render HTML.
