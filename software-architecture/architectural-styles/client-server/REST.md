# REST

## REST (Representational State Transfer)

- client-server architectural style often used to design web services/APIs

## Terms

### General

- **API**
- **caching**
- **client**
- **resource**
- **server**
- **state**
- **stateless**: data is stored outside the server
- **uniform resource identifier (URI)**

### JavaScript

- **Asynchronous JavaScript and XML (Ajax)**
- **XMLHttpRequest**: API that creates Ajax requests & sends them to a server

## Architectural constraints

1. use of client-server architecture
1. stateless - all data to fulfill a request is provided by the client
1. clients can cache responses
1. the API can run behind other layers, e.g. a proxy or load balancer
1. the API can return code on demand that can be used to extend the client
1. uniform interface - includes using URIs

## Client requests

- use HTTP keywords
  - **GET** (most common): fetch data & return it to the client
    - should only get data without any additional effects
  - **POST**: add a new resource
  - **PUT**: update single resource with provided URI/ID
    - usually implemented by replacing the entire object with the object provided in the request
  - **PATCH**: update single resource with provided URI/ID
    - usually implemented by updating only the fields provided in the request
  - **DELETE**: remove the resource with provided URI/ID
    - the DELETE keyword doesn't specify how/when the resource will be deleted

## Server responses

- server receives requests by listening to a specific address or port
- server routes each request to the code that can handle it
- return HTTP status codes
  - **2xx**: successful response
  - **4xx**: client error
  - **5xx**: server error
- common HTTP status codes
  - **200**: ok
  - **201**: resource created
  - **204**: no content
  - **400**: bad request
  - **401**: client is not authorized
  - **404**: server couldn't find requested resource
  - **500**: generic internal server error

## Working with databases

- various approaches:
  - each URI maps to a database table (common)
  - URI maps to a custom resource with data from multiple db tables

## Implementation

### Client

- JavaScript - most common consumer of REST APIs
  - uses the XMLHttpRequest object & Ajax
- other modern languages can consume REST APIs

### Server

- JSON - common format for server responses
- common languages for developing server functionality:
  - JavaScript/Node.js
    - usually using Express
  - Python
  - Java
  - PHP
  - C#/.NET
  - Go
