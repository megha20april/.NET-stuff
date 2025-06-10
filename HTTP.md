
## 🌐 What is an HTTP Request?

**HTTP (HyperText Transfer Protocol)** is the way browsers (or any client) **talk to servers** over the internet.

An **HTTP request** is a message that your browser or app sends to a server, asking it to do something.

---

## 📦 A Basic HTTP Request Contains:

| Part        | Description                                            |
| ----------- | ------------------------------------------------------ |
| **Method**  | What action you want to perform (e.g. GET, POST)       |
| **URL**     | The address of the resource you're asking for          |
| **Headers** | Extra info like content type, authentication, etc.     |
| **Body**    | The actual data (only for some types like POST or PUT) |

---

## 🧭 Common HTTP Request Methods (aka HTTP Verbs)

Here are the main ones you’ll use as a web dev:

| Method      | Purpose                             | Sends Data?           | Bookmarked? | Cached? | Idempotent? |
| ----------- | ----------------------------------- | --------------------- | ----------- | ------- | ----------- |
| **GET**     | Get/read something from the server  | ❌ Data in URL         | ✅ Yes       | ✅ Yes   | ✅ Yes       |
| **POST**    | Send data to create something       | ✅ Body                | ❌ No        | ❌ No    | ❌ No        |
| **PUT**     | Send data to update something fully | ✅ Body                | ❌ No        | ❌ No    | ✅ Yes       |
| **PATCH**   | Update part of something            | ✅ Body                | ❌ No        | ❌ No    | ✅ Yes       |
| **DELETE**  | Delete something                    | Sometimes (ID in URL) | ❌ No        | ❌ No    | ✅ Yes       |
| **HEAD**    | Get metadata without body           | ❌                     | ❌           | ✅       | ✅           |
| **OPTIONS** | Ask server what it allows           | ❌                     | ❌           | ❌       | ✅           |

---

## 🔍 Let’s Break That Down

### 🔵 1. **GET**

* Used to **read** data (like showing your diary entries).
* Data is sent via **URL query strings or Route Parameters**:

  ```
  /entries?page=2&sort=date
  or
  /:id
  ```
* Can be **bookmarked** (since all data is in the URL).
* Can be **cached** (e.g., browsers can save the response).
* Can be repeated safely — it **won’t change** anything.


---

### 🟠 2. **POST**

* Used to **create** new data (like submitting a form).
* Data is sent in the **body** of the request (not the URL).
* **Can’t be bookmarked** (because body data isn’t in the URL).
* **Not cached** by default.
* Not idempotent: multiple clicks can submit the same form twice.

---

### 🟢 3. **PUT**

* Used to **replace** an existing resource completely.
* Sends data in the **body**.
* Not cached or bookmarked.
* **Idempotent**: sending the same PUT request twice has the same effect.

---

### 🟣 4. **PATCH**

* Like PUT, but it **partially updates** a resource.
* Used for performance or targeted changes.
* Also idempotent (doing it twice = same result).

---

### 🔴 5. **DELETE**

* Deletes a resource.
* Usually uses the **ID in the URL**.
* Not cached or bookmarked.
* Idempotent: deleting something twice doesn't cause an error.

---

## 🧾 Where Does the Data Go?

| Method             | Data Location                               |
| ------------------ | ------------------------------------------- |
| **GET**            | In the **URL query string or route parameters** (visible!)      |
| **POST/PUT/PATCH** | In the **request body** (invisible to user) |
| **DELETE**         | Usually in the URL path                     |

Example:
 
```http
POST /diary/add
Content-Type: application/json

{
  "title": "My day",
  "content": "It was sunny"
}
```

---

## 💾 Caching

* **GET** requests can be cached by browsers and proxies to save load time.
* **POST/PUT/DELETE** are **not cached** (by default).
* You can use headers like `Cache-Control` and `ETag` to manage caching.

---

## 🔖 Bookmarking

Only **GET** requests can be bookmarked because all data is in the URL.

You can bookmark this:

```
https://mysite.com/entries?page=2&filter=important
```

But you **can’t bookmark a POST request**, because it doesn’t show in the address bar.

---

## ✅ Idempotency (cool word, simple idea)

An operation is **idempotent** if doing it multiple times gives the **same result**.

| Request | Idempotent? | Why?                                         |
| ------- | ----------- | -------------------------------------------- |
| GET     | ✅           | Reading is safe.                             |
| PUT     | ✅           | Updating to the same data does nothing new.  |
| DELETE  | ✅           | Deleting something twice is still “deleted”. |
| POST    | ❌           | Submitting twice creates duplicates.         |

---

## 🎯 Use-Cases Summary

| Scenario                       | Use          |
| ------------------------------ | ------------ |
| Load a web page                | GET          |
| Submit a form (login, contact) | POST         |
| Update user profile            | PUT or PATCH |
| Delete a blog post             | DELETE       |
| Get available methods/options  | OPTIONS      |

---
