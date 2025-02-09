# API - Application Programming Interface

API is interface to data stored somewhere in internet.

## Basics of API

An API (Application Programming Interface) allows different software applications to communicate with each other. It defines the methods and data formats that applications can use to request and exchange information.

## HTTP

HTTP (Hypertext Transfer Protocol) is the foundation of any data exchange on the Web and a protocol used for transmitting hypertext requests and information on the internet. It is the protocol used by web browsers and servers to communicate. Protocol - set of rules. 

### HTTP Methods

- **GET**: Requests data from a specified resource.
- **POST**: Submits data to be processed to a specified resource.
- **PUT**: Updates a current resource with new data.
- **DELETE**: Deletes the specified resource.
- **HEAD**: Asks for a response identical to a GET request, but without the response body. Used to check endpoint itself - to check if information there is correct.
- **OPTIONS**: Describes the communication options for the target resource.
- **PATCH**: Applies partial modifications to a resource.
- **CONNECT**: Establishes a tunnel to the server identified by the target resource.
- **TRACE**: Performs a message loop-back test along the path to the target resource.

### Features of HTTP Methods

HTTP methods have different characteristics and features that define their behavior:

- **Safe**: Methods that do not modify resources (e.g., GET, HEAD).
- **Idempotent**: Methods that can be called multiple times without different outcomes (e.g., GET, PUT, DELETE). This means that making multiple identical requests will have the same effect as making a single request.
- **Cacheable**: Methods that allow responses to be stored and reused (e.g., GET, HEAD).

### HTTP Methods Comparison

| Method   | Safe | Idempotent | Uses Body | Description                                                                 |
|----------|------|------------|-----------|-----------------------------------------------------------------------------|
| **GET**  | Yes  | Yes        | No        | Requests data from a specified resource.                                    |
| **POST** | No   | No         | Yes       | Submits data to be processed to a specified resource.                       |
| **PUT**  | No   | Yes        | Yes       | Updates a current resource with new data.                                   |
| **DELETE**| No  | Yes        | No        | Deletes the specified resource.                                             |
| **HEAD** | Yes  | Yes        | No        | Asks for a response identical to a GET request, but without the response body.|
| **OPTIONS**| Yes| Yes        | No        | Describes the communication options for the target resource.                |
| **PATCH**| No   | No         | Yes       | Applies partial modifications to a resource.                                |
| **CONNECT**| No | No         | No        | Establishes a tunnel to the server identified by the target resource.       |
| **TRACE**| No   | Yes        | No        | Performs a message loop-back test along the path to the target resource.    |

### HTTP Request Structure

An HTTP request consists of the following parts:

- **Request Line**: Contains the HTTP method, the resource URL, and the HTTP version.
  
  ```http
  GET /resource HTTP/1.1
  ```

- **Headers**: Provide additional information about the request.
  
  ```http
  Host: example.com
  Content-Type: application/json
  ```

- **Body**: Contains the data to be sent to the server (used with methods like POST, PUT, PATCH).

  ```json
  {
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
  ```

### HTTP Response Structure

An HTTP response consists of the following parts:

- **Status Line**: Contains the HTTP version, the status code, and the status message.
  
  ```json
  HTTP/1.1 200 OK
  ```

- **Headers**: Provide additional information about the response.
  
  ```json
  Content-Type: application/json
  ```

- **Body**: Contains the data sent back from the server.
  
  ```json
  {
    "id": 1,
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
  ```

### HTTP Status Codes Explanation

HTTP status codes are issued by a server in response to a client's request made to the server. They are grouped into five classes:

- **1xx Informational**: The request was received, continuing process.
  - **100 Continue**: The server has received the request headers, and the client should proceed to send the request body.
  - **101 Switching Protocols**: The requester has asked the server to switch protocols and the server has agreed to do so.

- **2xx Success**: The action was successfully received, understood, and accepted.
  - **200 OK**: The request has succeeded.
  - **201 Created**: The request has been fulfilled and resulted in a new resource being created.
  - **204 No Content**: The server successfully processed the request, but is not returning any content

- **3xx Redirection**: Further action needs to be taken in order to complete the request.
  - **301 Moved Permanently**: The URL of the requested resource has been changed permanently.
  - **302 Found**: The requested resource resides temporarily under a different URL.

- **4xx Client Error**: The request contains bad syntax or cannot be fulfilled.
  - **400 Bad Request**: The server could not understand the request due to invalid syntax.
  - **401 Unauthorized**: The client must authenticate itself to get the requested response.
  - **404 Not Found**: The server can not find the requested resource.

- **5xx Server Error**: The server failed to fulfill an apparently valid request.
  - **500 Internal Server Error**: The server has encountered a situation it doesn't know how to handle.
  - **503 Service Unavailable**: The server is not ready to handle the request.

## Postman

Postman is a popular API client that makes it easy for developers to create, share, test, and document APIs. It simplifies each step of building an API and streamlines collaboration so you can create better APIs faster.

### Endpoint

Endpoint is the end of a communication channel. The address of the URL to which we send the request to.

### Collections in Postman

A collection in Postman is a group of saved requests that can be organized into folders. Collections help you organize your requests and share them with your team. Each request in a collection can include details such as the HTTP method, URL, headers, and body. Collections can also include scripts to automate testing and workflows.

### Set as Variables and Variable Scope in Postman

Postman allows you to use variables to store and reuse values in your requests. Variables can be set manually or dynamically using scripts.

- **Set as Variables**: You can set variables in Postman by selecting text in a request or response and using the "Set as variable" option. This allows you to save the selected value as a variable for reuse in other requests.

- **Variable Scope**: Variables in Postman have different scopes, which determine their availability:
  - **Global**: Available across all collections and environments.
  - **Collection**: Available only within the specific collection.
  - **Environment**: Available only within the specific environment.
  - **Local**: Available only within the specific request or script.

Variables in Postman are presented with double curly braces `{{}}`. For example, a variable named `baseUrl` would be used as `{{baseUrl}}` in your requests.

### Changing Variables

You can change variables dynamically using scripts. For example, to change a global variable in a pre-request script:

```javascript
pm.globals.set("variableName", "newValue");
```

Alternatively, you can edit variables directly within a collection:

1. Click on the three dots (`...`) next to the collection name.
2. Select "Edit".
3. Go to the "Variables" tab.
4. Find the variable you want to change and update its value.
5. Save the changes.

### Initial Value vs Current Value

In Postman, variables can have both an initial value and a current value:

- **Initial Value**: This is the value that is shared when you export or share the collection. It is also the value that is used when you reset the variable.
- **Current Value**: This is the value that is used during runtime. It is not shared when you export or share the collection.

The initial value is useful for setting default values that can be shared with others, while the current value allows you to override these defaults during testing without affecting the shared collection.

Using variables and understanding their scope helps you manage and reuse values efficiently, making your API testing more dynamic and maintainable.

### Visualizing Responses in Postman

Postman provides several ways to visualize and analyze the responses from your API requests:

- **Pretty**: Formats the response in a readable way with proper indentation and syntax highlighting. This is useful for JSON, XML, and HTML responses.
- **Raw**: Displays the response as plain text without any formatting. This is useful for viewing the raw data returned by the server.
- **Preview**: Renders the response as a web page. This is useful for viewing HTML responses as they would appear in a browser.
- **Visualize**: Allows you to create custom visualizations of your response data using HTML, CSS, and JavaScript. You can use this feature to create charts, graphs, and other visual representations of your data.

To switch between these views, use the tabs at the bottom of the response section in Postman.

Using these visualization options helps you better understand and analyze the data returned by your API, making it easier to debug and improve your API.
