# MVC (Model–View–Controller)
MVC is a software architecture pattern (design pattern) that structures an application into three main components:

## 1. Model
- Represents the data and business logic
- Handles database operations, validations, and rules
- ex: C# classes + Entity Framework

## 2. View
- Represents the user interface
- Displays data from the Model to the user
- Handles no logic beyond basic data rendering
- ex: Razor `.cshtml` templates

## 3. Controller
- Manages application flow
- Handles user input (like HTTP requests)
- Calls the appropriate Model logic and returns a View response
- ex: C# classes handling routing/actions

### Simplified Flow:
> Request → Controller → Model → View → Response
