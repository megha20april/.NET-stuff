# View Template

- In ASP.NET core, a view template is a file that defines the HTML output users see in the browser.
- It's written in Razor syntax that mixes HTML and C#.
- File Extension: .cshtml

  Inside the Views folder, you'll usually see:

```
Views/
├── Home/
│   ├── Index.cshtml      ← Action method: HomeController.Index()
│   └── About.cshtml
├── Shared/
│   └── _Layout.cshtml    ← Master layout (like a base HTML shell)
```
- views are grouped by controller name
- the filename usually matches the Action method name
- `Shared/` is for common layouts or partials used across multiple views.
