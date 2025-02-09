# JavaScript Basics

## Comments in JavaScript

Comments are used to explain code and make it more readable. They are ignored by the JavaScript engine and do not affect the execution of the code.

### Single-line Comments

Single-line comments start with `//`. Everything after `//` on that line is considered a comment.

**Example**:

```javascript
// This is a single-line comment
let x = 5; // This is also a single-line comment
```

### Multi-line Comments

Multi-line comments start with `/*` and end with `*/`. Everything between `/*` and `*/` is considered a comment.

**Example**:

```javascript
/*
  This is a multi-line comment.
  It can span multiple lines.
*/
let y = 10;
```

## Console Methods

The `console` object provides access to the browser's debugging console. It includes several methods for logging information, clearing the console, and more.

### console.log()

The `console.log()` method is used to print messages to the console. It is commonly used for debugging purposes.

**Example**:

```javascript
console.log("Hello, world!");
let a = 10;
console.log("The value of a is:", a);
```

### console.clear()

The `console.clear()` method is used to clear the console.

**Example**:

```javascript
console.clear();
```

### Other Console Methods

- **console.error()**: Outputs an error message to the console.

  ```javascript
  console.error("This is an error message");
  ```

- **console.warn()**: Outputs a warning message to the console.

  ```javascript
  console.warn("This is a warning message");
  ```

- **console.info()**: Outputs an informational message to the console.
  
  ```javascript
  console.info("This is an informational message");
  ```

- **console.table()**: Displays data as a table in the console.

  ```javascript
  let users = [
    { name: "John", age: 30 },
    { name: "Jane", age: 25 }
  ];
  console.table(users);
  ```

- **console.time()** and **console.timeEnd()**: Starts and stops a timer, respectively. Used to measure the time taken by a block of code.
  
  ```javascript
  console.time("Timer");
  // Code to measure
  console.timeEnd("Timer");
  ```

## Variables in JavaScript

Variables are used to store data values. In JavaScript, you can declare variables using `var`, `let`, or `const`.

### Naming Conventions for Variables

- Variable names can contain letters, digits, underscores, and dollar signs.
- Variable names must begin with a letter, underscore, or dollar sign.
- Variable names are case-sensitive (e.g., `myVar` and `myvar` are different variables).
- Variable names should be descriptive and use camelCase (e.g., `firstName`, `totalAmount`).

### Variable Types

- **var**: Declares a variable, optionally initializing it to a value. Variables declared with `var` are function-scoped or globally-scoped.
- **let**: Declares a block-scoped local variable, optionally initializing it to a value. Variables declared with `let` are block-scoped.
- **const**: Declares a block-scoped, read-only named constant. The value of a `const` variable cannot be changed through reassignment.

### Differences Between `let`, `var`, and `const`

- **Scope**:
  - `var` is function-scoped or globally-scoped.
  - `let` and `const` are block-scoped.
- **Reassignment**:
  - `var` and `let` can be reassigned.
  - `const` cannot be reassigned.
- **Hoisting**:
  - `var` variables are hoisted to the top of their scope and initialized with `undefined`.
  - `let` and `const` variables are hoisted but not initialized.

**Examples**:

```javascript
// var example
var x = 10;
if (true) {
  var x = 20; // same variable
}
console.log(x); // 20

// let example
let y = 10;
if (true) {
  let y = 20; // different variable
}
console.log(y); // 10

// const example
const z = 10;
z = 20; // Error: Assignment to constant variable.
```

## Data Types in JavaScript

JavaScript has dynamic types, meaning variables can hold values of different types at different times. The following are the data types in JavaScript:

### Primitive Data Types

1. **String**: Represents textual data.
   - **Example**: `"Hello, world!"`
2. **Number**: Represents both integer and floating-point numbers.
   - **Example**: `42`, `3.14`
3. **Boolean**: Represents a logical entity and can have two values: `true` or `false`.
   - **Example**: `true`, `false`
4. **Undefined**: Represents a variable that has been declared but not assigned a value.
   - **Example**: `let a; console.log(a); // undefined`
5. **Null**: Represents the intentional absence of any object value.
   - **Example**: `let b = null;`
6. **Symbol**: Represents a unique and immutable value.
   - **Example**: `let sym = Symbol("description");`
7. **BigInt**: Represents integers with arbitrary precision.
   - **Example**: `let bigInt = 1234567890123456789012345678901234567890n;`

### Non-Primitive Data Types

1. **Object**: Represents a collection of properties, where each property is a key-value pair.
   - **Example**:

     ```javascript
     let person = {
       firstName: "John",
       lastName: "Doe",
       age: 30
     };
     ```

## String Methods

Strings in JavaScript are used to represent and manipulate text. Here are some commonly used string methods:

### Concatenation

Concatenation is the process of joining two or more strings together.

**Example**:

```javascript
let firstName = "John";
let lastName = "Doe";
let fullName = firstName + " " + lastName;
console.log(fullName); // "John Doe"
```

### String Interpolation

String interpolation is a way to embed expressions within string literals, using template literals. Template literals are enclosed by backticks (`` ` ``) instead of single or double quotes.

**Example**:

```javascript
let firstName = "John";
let lastName = "Doe";
let fullName = `${firstName} ${lastName}`;
console.log(fullName); // "John Doe"
```

String interpolation allows you to include variables and expressions directly within the string, making it more readable and easier to manage.

### Splitting

The `split()` method splits a string into an array of substrings based on a specified separator.

**Example**:

```javascript
let str = "Hello, world!";
let words = str.split(" ");
console.log(words); // ["Hello,", "world!"]
```

### Trimming

The `trim()` method removes whitespace from both ends of a string.

**Example**:

```javascript
let str = "   Hello, world!   ";
let trimmedStr = str.trim();
console.log(trimmedStr); // "Hello, world!"
```

### Substring

The `substring()` method extracts a part of a string between two specified indices.

**Example**:

```javascript
let str = "Hello, world!";
let subStr = str.substring(0, 5);
console.log(subStr); // "Hello"
```

### Replacing

The `replace()` method replaces a specified value with another value in a string.

**Example**:

```javascript
let str = "Hello, world!";
let newStr = str.replace("world", "JavaScript");
console.log(newStr); // "Hello, JavaScript!"
```

### Changing Case

The `toUpperCase()` and `toLowerCase()` methods convert a string to uppercase and lowercase, respectively.

**Example**:

```javascript
let str = "Hello, world!";
console.log(str.toUpperCase()); // "HELLO, WORLD!"
console.log(str.toLowerCase()); // "hello, world!"
```

## Number Methods and Operations

Numbers in JavaScript are used to perform mathematical operations. Here are some commonly used number methods and operations:

### Basic Arithmetic Operations

- **Addition (`+`)**: Adds two numbers.

  ```javascript
  let sum = 5 + 3;
  console.log(sum); // 8
  ```

- **Subtraction (`-`)**: Subtracts one number from another.

  ```javascript
  let difference = 5 - 3;
  console.log(difference); // 2
  ```

- **Multiplication (`*`)**: Multiplies two numbers.

  ```javascript
  let product = 5 * 3;
  console.log(product); // 15
  ```

- **Division (`/`)**: Divides one number by another.

  ```javascript
  let quotient = 5 / 3;
  console.log(quotient); // 1.6666666666666667
  ```

- **Modulus (`%`)**: Returns the remainder of a division.

  ```javascript
  let remainder = 5 % 3;
  console.log(remainder); // 2
  ```

### Increment and Decrement

- **Increment (`++`)**: Increases a number by one.

  ```javascript
  let x = 5;
  x++;
  console.log(x); // 6
  ```

- **Decrement (`--`)**: Decreases a number by one.

  ```javascript
  let x = 5;
  x--;
  console.log(x); // 4
  ```

### Number Methods

- **`toFixed()`**: Formats a number to a specified number of decimal places.

  ```javascript
  let num = 5.6789;
  console.log(num.toFixed(2)); // "5.68"
  ```

- **`parseInt()`**: Parses a string and returns an integer.

  ```javascript
  let str = "123";
  let num = parseInt(str);
  console.log(num); // 123
  ```

- **`parseFloat()`**: Parses a string and returns a floating-point number.

  ```javascript
  let str = "123.45";
  let num = parseFloat(str);
  console.log(num); // 123.45
  ```

Understanding and using string methods and number methods effectively helps you manipulate and work with data in JavaScript, making your code more powerful and flexible.
