# REST

## REST (Representational State Transfer)

- client-server architectural style often used to design web services/APIs
- invented in 2000

## Terms

### General

- **API**
- **caching**
- **client**
- **idempotency**: concept of an operation always producing the same result
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

## REST URLs

- usually https or http
- default ports: **443** (https), **80** (http)
  - local dev environments may use different defaults
- path naming conventions
  - **/api** (optional)
  - **/\<versionInfo\>** (optional) - ex. **/v1**
  - **/\<resources\>** - name of resource, plural; ex. **/customers**
    - collection paths end here
  - **/\<id\>** - identifier for single specific resource; ex. **/745**
  - **/\<subcollection\>** - subcollections in a single resource
    - ex. **/orders/196/items**
    - ex. **/courses/82/students/27** - path to single item in subcollection
  - **?\<params\>** - 1 or more query params (optional)
    - query values are comma-separated
      - ex. **?include=images,reviews**
    - queries are &-separated
      - ex. **?take=25&start=51** (pagination)

## Client requests

- parts of a request:
  - headers
    - **Accept**: desired content type of response data
    - **Content-Type**: format of data being sent to the server
  - HTTP keyword
  - URL
  - query parameters
- HTTP keywords
  - **GET** (most common): fetch data & return it to the client
    - should only get data without any additional effects
  - **POST**: add a new resource
    - if successful, server typically returns the id of the new object
  - **PUT**: update single resource by replacing/updating the entire object
    - idempotent
    - consistently supported by languages with REST implementations
  - **PATCH**: update single resource by updating part of the object
    - recommended to be idempotent, but implementations vary
    - has less support from languages than PUT
  - **DELETE**: remove the resource
    - DELETE keyword doesn't specify how/when the resource will be deleted

## Server responses

- server receives requests by listening to a specific address or port
- server routes each request to the code that can handle it
- parts of a response:
  - http status code - always returned
  - headers
    - **Content-Type**: format of data in the response
  - data
  - message
- return HTTP status codes
  - **1xx**: informational (rarely used)
  - **2xx**: successful response
  - **3xx**: redirection
  - **4xx**: client error
  - **5xx**: server error
- most common HTTP status codes
  - **200**: ok - common with GET; response body usually contains data
  - **201**: created - common with POST
  - **204**: no content - common with DELETE/PUT/PATCH
  - **400**: bad request - generic error
  - **404**: not found
  - **500**: internal server error - generic error
- other notable HTTP status codes
  - **301**: moved permanently
  - **304**: not modified
  - **307**: temporary redirect
  - **401**: unauthorized - client is not authenticated
  - **403**: forbidden - authenticated but incorrect permissions
  - **405**: method not allowed - HTTP keyword is not supported by the endpoint
  - **406**: not acceptable - client requests the response in an unsupported media type
  - **415**: unsupported media type - client request uses an unsupported media type
  - **501**: not implemented; often used to communicate "coming soon"

## Content types

- specified as **\<category\>\\\<type\>** in request & response headers
- server is not required to honor the content type in a request's Accept header
- servers are strict about which content types are supported
- most commonly used subtypes:
  - **JSON** (application/json)
  - **XML** (application/xml)
- most common categories:
  - **text**: human-readable; ex. CSS, HTML, JavaScript
  - **font**
  - **application**: binary data that doesn't fit into other categories or requires a specific app to use it
  - **audio**
  - **image**
  - **video**

## Working with databases

- CRUD db operations
  - GET - read
  - DELETE - delete
  - POST - create
  - PUT/PATCH - update
- URL approaches:
  - each URL maps to a database table (common)
  - URL maps to a custom resource with data from multiple tables

## Design

### Connectivity

- handle retrying connections if expected clients have slow or unreliable connections (ex. mobile)

### Server

- can be dynamic (more common) or static
  - **dynamic** - tied to data that can be changed by clients
  - **static** - tied to data that can't be changed by clients
- keep response size to a minimum by including only necessary data
  - improves ux
  - some clients have minimal computing power

## Implementation

### Client

- JavaScript - most common consumer of REST APIs
  - uses the XMLHttpRequest object & Ajax
- other modern languages can consume REST APIs

### Server

- most modern languages are suitable for building REST APIs, e.g.:
  - JavaScript/TypeScript/Node.js
    - usually uses Express framework
  - Python
  - Java
  - PHP
  - C#/.NET
  - Go
  - Ruby
  - Kotlin
- JSON - common format for server responses

### Errors

- For security purposes, minimize info given in 401 and 5xx error messages

### Security

- use https
