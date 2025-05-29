
## .csproj File of the application

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

</Project>
```
- Project line tells .net that this is a web project using the web sdk which includes everything needed to develop asp.net web applications.
- PropertyGroup --> this is just a section in which you define properties for your project.
- TargetFramework --> determines which version of .net should be used to run this application.
- Nullable enable --> enables nullable reference types, a C# feature that helps prevent null reference exceptions by making the compiler warn you about potential null values. It's a safety feature that helps catch bugs early.
- Implicit Usings enabled --> This automatically includes common using statements (like System, System.Collections.Generic, etc.) so you don't have to write them at the top of every C# file. It reduces boilerplate code.

> #### How is this file read?
>
> - This file is read by MSBuild (microsoft's build engine that comes with .net sdk)
> - in the first line, when we specify the .net sdk, msbuild imports predefined xml files, that define what tags are valid and what they do.
> - if we use an invalid tag, msbuild will either ignore it or give you an error.

---

## Connected Services

- A visual studio wizard/helper tool that connects your app to external services without manual setup.
- It allows developers to connect their application to various services like Rest APIs, databases (sql server, azure sql etc.), cloud services, etc..
- Provides a centralized location to manage all connected services.
- It basically automates these tasks, which we would've done manually if not for this tool:
      - adds the necessary nuget packages for the service.
      - generates their config code
      - updates appsettings.json file
      and other setup things....

---

## Dependencies

- all the external code libraries (packages) that your projects are listed here.
- this is not an actual folder or anything, it's just a visual representation of all the referenced packages of our project.
- frameworks --> shows the frameworks your project use like, .net and asp.net core etc.
- packages --> your nuget package references, points to the global cache locations.
- analyzers --> special packages that analyze your code while you write them, they run during compilation to give warnings/suggestions. also stored globally.

---

## Properties/

contains the config files for your proj.

## launchSettings.json

- tells ide, how to run your web application.
- $schema: provides a url to a JSON schema, which lets the IDEs validate the structure of this file and thus give suggestions and errors.

- profiles - each profile defined in this section provides a diff way to launch the application during development. Profiles can specify settings like the application url, env variables, whether to lauch the browser or not, and more. By default, it comes with three profiles:

  1. HTTP Launch Profile:
    - `commandName: "Project"` --> indicates the application should be run directly without IIS Express server.
    - `launchBrowser: true` --> browser automatically opens when proj starts.
    - `environmentVariables` --> used to set env vars that are essential during the dev phase. For ex, `ASPNETCORE_ENVIRONMENT` that can be set to Development, Staging or Production.
    - `dotnetRunMessages: true` --> enables helpful messages to be displayed when the project is built and run using the .NET CLI.
    - `applicationUrl` -> url to access the application.

  2. HTTPS Launch Profile:
    - `applicationUrl: “https://localhost:7107;http://localhost:5066”` --> This means the application will listen on both HTTP (http://localhost:5066) and HTTPS (https://localhost:7107). HTTPS is preferred for secure communication.

  3. IIS Express Launch Profile:
    - `commandName: “IISExpress”` --> indicates that application will run under IIS Express, a lightweight, self-contained version of IIS that is optimized for the development environment.

- IIS Settings --> setting that will be used by the IIS Express profile
    - `windowsAuthentication: false` – Indicates that Windows Authentication is disabled. If set to true, Windows Authentication is enabled.
    - `anonymousAuthentication: true` – Specifies whether Anonymous Authentication is enabled for your application. Setting it to true means any user can access the application without credentials.
    - `applicationUrl: http://localhost:53952` – Specifies the base URL for the application under IIS Express, like “http://localhost:53952”.
    - `sslPort: 44312` – Specifies the port to use for SSL (HTTPS) traffic when using IIS Express. If the value is 0, the application cannot be accessed using HTTPS.

- iis -> internet information service used for running and testing applications locally without hosting it on a separate server.
  
> Questions:
> - what is IIS?
> - How is a proj run directly i.e. without using IIS?
> - what is SSL?
> - what is SSL port?

---

## wwwroot

- root of your website, from the browser's perspective.
- serves static files (files that never change), you can access them with a url, `<localhostUrl>/js/site.js` etc.
- these files that the browser can directly access.
- also images, fonts or any other assets.
- web server automatically serves these files.

---

## appsettings.json

[dot net tutorials article about it](https://dotnettutorials.net/lesson/asp-net-core-appsettings-json-file/)
