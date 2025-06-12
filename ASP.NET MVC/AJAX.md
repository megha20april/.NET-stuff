# What Happens Normally (Without AJAX)?

When you submit a form or click a link that sends a request to the server, the browser reloads the entire page to show the response. This is called a synchronous request — it waits for the server to respond and replaces the whole page content.


# 🚀 What AJAX Does Differently

AJAX stands for Asynchronous JavaScript and XML, and its goal is:

✅ Send a request to the server
✅ Receive a response
✅ Update part of the page, not reload the whole page

# 🔧 But How Does AJAX Do That?

AJAX uses JavaScript’s XMLHttpRequest or the newer fetch() or Jquery's $.ajax() API to:
Send an HTTP request behind the scenes (in the background).
Receive the server's response (usually JSON or HTML).
Use JavaScript to update the DOM — which means it changes content on the page using things like:

```js
document.getElementById("result").innerHTML = responseData;
```

> ➡️ The key part: The browser doesn't reload the page because JavaScript intercepts the request and directly manipulates the existing content.



# AJAX Helpers
- JQuery Unobtrusive AJAX library provides the AJAX helpers in Razor views

## 🧠 Why Do I Need AJAX Helpers?

You need AJAX helpers in ASP.NET Core MVC when you:
✅ Want to do partial updates to the page without reloading
✅ Want to use Razor syntax to simplify generating HTML and wiring up JS
✅ Want to avoid manually writing JS code for every form or link

## What would i need to do if i don't use them?

In Razor:

```html
<form id="myForm">
    <input type="text" name="name" />
    <button type="submit">Submit</button>
</form>
<div id="resultDiv"></div>

<script>
document.getElementById("myForm").addEventListener("submit", function (e) {
    e.preventDefault(); // stop normal post
    fetch('/Home/GetGreeting', {
        method: 'POST',
        body: new FormData(this)
    })
    .then(res => res.text())
    .then(html => {
        document.getElementById('resultDiv').innerHTML = html;
    });
});
</script>
```

In controller:

```csharp
[HttpPost]
public IActionResult GetGreeting(string name)
{
    return PartialView("_GreetingPartial", name);
}
```

Partial View (_GreetingPartial.cshtml):

```html
<p>Hello, @Model!</p>
```

✅ Works perfectly, but requires manual JS every time.

## Now with AJAX helpers, I can just do

```csharp
@using (Ajax.BeginForm("GetGreeting", "Home",
    new AjaxOptions {
        HttpMethod = "POST",
        UpdateTargetId = "resultDiv",
        InsertionMode = InsertionMode.Replace
    }))
{
    <input type="text" name="name" />
    <input type="submit" value="Say Hello" />
}
```
It renders to plain HTML with extra data- attributes:

```html
<form action="/Home/GetGreeting"
      data-ajax="true"
      data-ajax-method="POST"
      data-ajax-update="#resultDiv"
      data-ajax-mode="replace"
      method="post">
    <input type="text" name="name" />
    <input type="submit" value="Say Hello">
</form>
```
This is now a special form: it will be caught by jQuery.Unobtrusive.Ajax.js.
who reads them and sends a AJAX request using $.ajax()
and injects response HTML into a DOM element

---

- Although these AJAX helpers look simpler but they are not that flexible.
- Hence, Explicit JS (jQuery) is more common and preferred today because throught them you control every part of the request.
- Microsoft considers these helpers legacy and has removed them from ASP.NET CORE as a default functionality.
