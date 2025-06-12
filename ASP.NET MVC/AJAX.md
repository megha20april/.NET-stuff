# What Happens Normally (Without AJAX)?

When you submit a form or click a link that sends a request to the server, the browser reloads the entire page to show the response. This is called a synchronous request — it waits for the server to respond and replaces the whole page content.


# 🚀 What AJAX Does Differently

AJAX stands for Asynchronous JavaScript and XML, and its goal is:

✅ Send a request to the server
✅ Receive a response
✅ Update part of the page, not reload the whole page

# 🔧 But How Does AJAX Do That?

AJAX uses JavaScript’s XMLHttpRequest or the newer fetch() API to:
Send an HTTP request behind the scenes (in the background).
Receive the server's response (usually JSON or HTML).
Use JavaScript to update the DOM — which means it changes content on the page using things like:

```js
document.getElementById("result").innerHTML = responseData;
```

> ➡️ The key part: The browser doesn't reload the page because JavaScript intercepts the request and directly manipulates the existing content.

