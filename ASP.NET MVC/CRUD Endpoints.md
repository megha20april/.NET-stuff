# What is an endpoint in Web Development?

- A specific URL/URI that a web application responds to.
- It is a point of interaction between the client and server.
- Ex. `/api/users`, `/api/products/{id}`, etc.

---

# Types of Endpoints

- **RESTful**  -- Representational State Transfer
- **GraphQL**  -- Graph Query Language
- **SOAP**     -- Simple Object Access Protocol

These are just protocols/rules to write api endpoints

### RESTful

- This protocol uses standard HTTP methods (GET, POST, PUT, DELETE) to interact with resources (like users, products, etc.)
- Commonly used in modern web APIs.

✅ Characteristics:
- Uses URLs to access resources.
- Data format is usually JSON.
- Each URL represents a resource (like /api/user, /order/1, /products)
- **Stateless**: The server doesn’t remember your previous request.



### GraphQL

- This protocol lets you ask for exactly what you want.
- This often has one endpoints
- To which you send queries asking for specific data.
- or mutations to change data.
- Request and response format is always JSON.

```graphql
query {
  user(id: "123") {
    name
    email
  }
}
```

### SOAP

- SOAP is an older, more strict protocol for building APIs. 
- It uses XML (not JSON), and is very formal, with a strong structure and rules.

```xml
<soap:Envelope>
  <soap:Body>
    <GetUser>
      <UserId>123</UserId>
    </GetUser>
  </soap:Body>
</soap:Envelope>
```