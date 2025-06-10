## Controllers

- A controller file in ASP.Net Core is a C# class that group related request handlers (like the router did in express) together.
- It's a way to organize routes into separate modules.

```
Project/
├── Controllers/
│   ├── HomeController.cs      // Handles /Home routes
│   ├── UsersController.cs     // Handles /Users routes
│   └── ProductsController.cs  // Handles /Products routes
```

- class names must match filename.
- The route prefix comes from removing "Controller" from the name ex. UsersController -> /Users

---

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

---

## Action Methods

- These methods are public methods inside controller. They handle all the routes of your controller.
- equivalent to `router.<method>('/<action>', handler);` in express
- ASP.NET Core action:

```csharp
public class UsersController : Controller
{
    // This method is an "action"
    public IActionResult Index()
    {
        var users = GetUsersFromDB();
        return Json(users);
    }
}
```

---

### IActionResult

- Responses of controllers can be anything from a simple status code, plain text, a view (HTML), a file, or even a JSON object.
- These responses are encapsulated in objects known as Action Results.
- In ASP.NET Core, the response objects implement IActionResult
- It is a base class of all the response types an action method returns.
- as it's an interface that represents the response object type of an action method.

#### Common IActionResult Implementations
As shown in the hierarchy below, various result types implement IActionResult either directly or through ActionResult:

```
IActionResult --> containes ExecuteResultAsync() which is implemented by everyone.
├── ActionResult (abstract) --> implements the methods of the interface, but its methdods get overriden
│   ├── ViewResult --> by View(), renders view templates
│   ├── PartialViewResult
│   ├── JsonResult  --> send back json data
│   ├── RedirectResult
│   ├── RedirectToActionResult
│   ├── ContentResult  ---> raw response, like in xml or text etc.
│   ├── FileResult   --> returns files
│   ├── StatusCodeResult  --> sends back http status code with message
│   ├── ObjectResult
│   │   ├── OkObjectResult  --> all of these have predefined http status codes associated with them
│   │   ├── BadRequestObjectResult
│   │   ├── NotFoundObjectResult
│   │   └── CreatedResult
│   └── EmptyResult   ---> returns nothing, we do this since most controller actions must return an IActionResult so that MVC knows what to send back to the client.
└── Other implementations...
```

#### Result Processing

The ASP.NET Core framework calls the ExecuteResultAsync method on the returned result:

```csharp
// Framework code (simplified)
var result = actionMethod.Invoke(); // Gets IActionResult
await result.ExecuteResultAsync(actionContext); // Generates HTTP response
```
---

#### Specific Return Types vs IActionResult

You can also use specific return types instead of the generic IActionResult when you know that the action will always return the same type.
```csharp
public class UsersController : Controller
{
    // Generic return type - can return anything
    public IActionResult Flexible()
    {
        if (someCondition)
            return View();
        else
            return Json(data);
    }
    
    // Specific return types - compile-time safety
    public ViewResult SpecificView() => View();
    public JsonResult SpecificJson() => Json(data);
    public RedirectResult SpecificRedirect() => Redirect("/");
    public ContentResult SpecificContent() => Content("Hello");
   
}
```
---

#### Route Mapping

Default Convention:
- UsersController.Index() → GET /Users
- UsersController.Details(int id) → GET /Users/Details/5
- UsersController.Create() → GET /Users/Create

---

### What happens when we do View()

ASP.NET MVC looks for a .cshtml file in:
`/Views/{ControllerName}/{ActionName}.cshtml`
ex.
`/Views/Home/About.cshtml` through About() action method of HomeController
