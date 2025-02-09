# Postman Scripts

Postman scripts allow you to automate tasks, manipulate data, and perform custom logic during your API testing. Scripts in Postman are written in JavaScript and can be used to enhance your API testing workflow.

## Types of Postman Scripts

### Pre-request Scripts

Pre-request scripts are executed before the request is sent. They are used to set up the environment, add dynamic data to the request, and perform any necessary setup tasks.

**Common Use Cases**:

- Setting or updating variables.
- Adding authentication tokens to the request headers.
- Generating dynamic data (e.g., timestamps, random values).
- Logging information for debugging purposes.

**Example**:

```javascript
// Set a variable
pm.environment.set("timestamp", new Date().toISOString());

// Add an authorization token to the request headers
pm.request.headers.add({ key: "Authorization", value: "Bearer " + pm.environment.get("authToken") });
```

### Post-response Scripts (Tests)

Post-response scripts, also known as tests, are executed after the response is received. They are used to validate the response, extract data, and perform any necessary cleanup tasks.

**Common Use Cases**:

- Validating the response status code.
- Checking the response body for specific values.
- Extracting data from the response and storing it in variables.
- Logging information for debugging purposes.

**Example**:

```javascript
// Validate the response status code
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Check the response body for a specific value
pm.test("Response contains user ID", function () {
    pm.expect(pm.response.json().id).to.eql(1);
});

// Extract data from the response and store it in a variable
var jsonData = pm.response.json();
pm.environment.set("userId", jsonData.id);
```

Using pre-request and post-response scripts in Postman helps you automate and streamline your API testing process, making it more efficient and effective.
