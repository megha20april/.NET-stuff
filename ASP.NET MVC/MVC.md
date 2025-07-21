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

![image](https://github.com/user-attachments/assets/65994045-cd93-453b-b18b-616a6034a853)


### Example Flow run
Router's job is to map a request path/url to a function

#### MPAs --> Multi Page Applications

In old-school web apps like ones built using:
EJS / Razor / JSP / PHP, etc.
All rendering happens on the server

Request: GET /users --> Router will map it to a function inside the controller --> getUsers(): this will interact with a model let's say, User --> the model works with the database (this is done using ORM or SQL) --> now the output, here a list of users, is returned to the controller --> controller then gives that output to views --> views have the responsibility of presenting that data --> view generates the html + css with the data embedded in it --> which is again returned back to the controller and then ultimately to the client

#### SPAs --> Single Page Applications

- Here routing happens two times, on client and on server side.
- The frontend and backend are decoupled.
- The frontend is usually served as static files (HTML, CSS, JS).
- Routing happens on the client (browser) using libraries like React Router, Vue Router, etc.
- Data is fetched separately via API calls.

Click /profile → React Router matches path → Loads Profile component → Calls backend API (like /api/user/123) → Frontend request → here comes our Server router which maps the request to → Controller → which then Returns JSON (by interacting with models and stuff) → Frontend renders UI using this returned data

> for ex., in node.js the express can be seen as a server router
