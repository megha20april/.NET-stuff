- .sln stands for Solution File.
- A solution contains a collection of Projects, along with dependencies between those projects.
- The projects themselves contain source files.
- You can have as many projects as you like in a solution, but there can be only one solution open at a time in a particular instance of VS.NET, meaning one window.
- You cannot nest one solution inside another.
- It tells the IDE:
    - what projects exist
    - how they are related
    - where they live on disk
    - what settings or configs are used for building
 
- .sln is a plain text file.

- Ex. of a solution
```
MySolution.sln
│
├── WebApp/         → ASP.NET Core frontend
│   └── WebApp.csproj
│
├── BackendAPI/     → API logic
│   └── BackendAPI.csproj
│
└── Tests/          → Unit tests
    └── Tests.csproj
```
> The .sln file sits at the top and keeps track of all these .csproj files.

.csproj file:
- C# project file in XML.
- consists of details like:
    - which .cs files to compile
    - what NuGet packages to include
    - defines the output type in the assembly of that proj. ex. .exe or .dll etc.
    - .NET framework version
    - Unique ID of that project
    - Output file name like, MyFirstProj.exe --> Assembly Name
    - Itemgroup (References) -> all the references for a proj ex. System, System.Net etc.
    - Itemgroup (Code Files) -> all the written source files
    - etc..
 - It's kinda similar to package.json in node.js
