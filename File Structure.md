- bin/ ---> final build output, i.e. .dll, .exe etc.
- obj/ ---> temporary /intermediate build files created by the compiler during the cuild process.

- All the nuget packages in .net are stored in a global cache memory.
- `C:\Users\<UserName>\.nuget\packages\`
- All the packages point to the same copy of packages in the global folder.
- This saves space.
- Everytime we do, `dotnet restore`, it checks the global cache first and if the package is already there, then we get a offline restore (faster and memory efficient)
  and if it doesn't find the package there, it installs it then.
- BUT If no project is using a NuGet package anymore, the package will still sit in the global NuGet cache — .NET does not automatically delete it.
  we have to manually delete the unused packages.
