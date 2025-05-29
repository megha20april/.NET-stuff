
## .NET SDK vs .NET runtime

- sdk contains all the libraries, compiler, command line tools, project templates and so on... required to develop .net applications. For developers.
- while on the other hand, .net runtime contains things like CLR, BCL, GC and JIT which are required to execute the applications only. For end users.

---

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

Connected Services
- A visual studio wizard/helper tool that connects your app to external services without manual setup.
- It allows developers to connect their application to various services like Rest APIs, databases (sql server, azure sql etc.), cloud services, etc..
- Provides a centralized location to manage all connected services.
- It basically automates these tasks, which we would've done manually if not for this tool:
      - adds the necessary nuget packages for the service.
      - generates their config code
      - updates appsettings.json file
      and other setup things....

Dependencies
- all the external code libraries (packages) that your projects are listed here.
- this is not an actual folder or anything, it's just a visual representation of all the referenced packages of our project.
- frameworks --> shows the .net runtime your apps targets/uses like .net 8.0. stored in the program files.
- packages --> your nuget package references, points to the global cache locations.
- analyzers --> special packages that analyze your code while you write them, they run during compilation to give warnings/suggestions. also stored globally.

Properties/launchSettings.json
- $schema: defines the format of launchSettings.json file, hence it allows us to edit this file by ensuring ide understands this file.
- iis -> internet information service used for running and testing applications locally without hosting it on a separate server.
- 


wwwroot
- serves static files, you can access them like this, `<localhostUrl>/js/site.js` etc.
- these files are not critical and is genrally client side
- also images, fonts or any other assets.
- also handles their caching.

