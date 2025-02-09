<!-- TOC -->

# Table of contents

- [Table of contents](#table-of-contents)
- [Setup](#setup)
  - [Installation commands](#installation-commands)
  - [Key folders \& Files](#key-folders--files)
- [Mocca and Hooks](#mocca-and-hooks)
- [Assertions](#assertions)
  - [should()](#should)
  - [and()](#and)
  - [expect()](#expect)
  - [Chainable getters](#chainable-getters)
- [Functions](#functions)
  - [Selecting elements](#selecting-elements)
    - [get()](#get)
    - [contains()](#contains)
    - [within()](#within)
  - [Traversal in JS and Cypress](#traversal-in-js-and-cypress)
  - [Actions](#actions)
    - [type()](#type)
    - [focus(), blur(), clear()](#focus-blur-clear)
    - [submit()](#submit)
    - [click()](#click)
    - [dblclick(), rightclick()](#dblclick-rightclick)
    - [check()](#check)
    - [uncheck()](#uncheck)
    - [select()](#select)
    - [scrollIntoView(), scrollTo()](#scrollintoview-scrollto)
    - [trigger](#trigger)
    - [Mouse actions - draggable(), droppable()](#mouse-actions---draggable-droppable)
  - [Location](#location)
    - [hash()](#hash)
    - [location()](#location-1)
    - [url()](#url)
  - [Navigation](#navigation)
    - [go('forward'), go('back'), go(-1), go(1)](#goforward-goback-go-1-go1)
    - [reload()](#reload)
    - [visit()](#visit)
  - [Window](#window)
    - [window()](#window-1)
    - [document()](#document)
    - [title()](#title)
  - [Misc](#misc)
    - [log()](#log)
    - [end()](#end)
    - [exec()](#exec)
    - [focused()](#focused)
    - [screenshot()](#screenshot)
    - [wrap()](#wrap)
    - [pause()](#pause)
    - [wait()](#wait)
    - [eq](#eq)
    - [Cookies and Local Storage](#cookies-and-local-storage)
  - [Connectors](#connectors)
    - [each()](#each)
    - [its()](#its)
    - [then()](#then)
    - [invoke()](#invoke)
    - [spread()](#spread)
  - [Files](#files)
    - [fixtures()](#fixtures)
    - [readFile(), writeFile()](#readfile-writefile)
  - [Network Requests](#network-requests)
    - [request()](#request)
    - [intercept()](#intercept)
    - [XHR Testing](#xhr-testing)
- [Aliasing](#aliasing)
- [Selectors](#selectors)
- [Plugins](#plugins)
  - [cypress XPath](#cypress-xpath)
  - [Cypress RETRIABILITY- Commes preinstalled in Cypress v5](#cypress-retriability--commes-preinstalled-in-cypress-v5)
  - [Cucumber preprocessor - Run cucumber/gherkin szntax with Cypress.io](#cucumber-preprocessor---run-cucumbergherkin-szntax-with-cypressio)
- [Tips and Tricks](#tips-and-tricks)
  - [Multiple tabs tricks](#multiple-tabs-tricks)
  - [Same origin trick](#same-origin-trick)
  - [Handling JS events / Alerts](#handling-js-events--alerts)
  - [Handling iframes](#handling-iframes)
  - [Environment Variables Options](#environment-variables-options)
  - [Global options](#global-options)
  - [Custom - Cypress.Commands.add()](#custom---cypresscommandsadd)
  - [Handling File upload](#handling-file-upload)
  - [Configuring Viewports](#configuring-viewports)
- [Scripts and configurations](#scripts-and-configurations)
  - [Making script in package.json](#making-script-in-packagejson)
  - [Different configurations](#different-configurations)
- [Reporting](#reporting)
- [Best Practices](#best-practices)
  - [Selecting element](#selecting-element)
  - [_cy.get_ vs _cy.find_](#cyget-vs-cyfind)

# Setup

## Installation commands

- Starting Cypress

  ```js
  npm init - initialization of package.json file where we can put all the neccessary information

  npm install - installs all the important files

  ./node_modules/.bin/cypress open - opens Cypress test runner
  ```

- _run_ trigger _ALL_ tests from command line via _Headless Electron_

  ```js
  ./node_modules/.bin/cypress run
  ```

- _run --headed_ trigger _ALL_ tests from command line via _Headed Browser Electron_

  ```js
  ./node_modules/.bin/cypress run --headed
  ```

- _run --browser chrome_ trigger _ALL_ tests from command line via \_Headed Browser Chrome

  ```js
  ./node_modules/.bin/cypress run --browser chrome
  ```

- _run --spec RELATIVE-PATH_ trigger _ONE_ test from command line via _Headless Electron_

  ```js
  ./node_modules/.bin/cypress run --spec RELATIVE-PATH
  ```

- _run --spec RELATIVE-PATH-TO-FOLDER/\*_ trigger _ONE_ test from command line via _Headless Electron_

  ```js
  ./node_modules/.bin/cypress run --spec RELATIVE-PATH-TO-FOLDER/*
  ```

- _npm install -g npx_ - Executes comnmand either from a local node_modules/.bin or from central cache. Simplifies executing

  ```js
  // When installed use
  npx cypress open // instead of ./node_modules/.bin/cypress open

  ```

- _npx cypress open --env configFile=staging_ - Switch environments

```js
// Make config folder with env configuraton file
// In plugins / index.js insert
const fs = require("fs-extra");
const path = require("path");

function getConfigurationByFile(file) {
  const pathToConfigFile = path.resolve("cypress", "config", `${file}.json`);

  if (!fs.existsSync(pathToConfigFile)) {
    console.log("No custom config file found.");
    return {};
  }

  return fs.readJson(pathToConfigFile);
}

// plugins file
module.exports = (on, config) => {
  // accept a configFile value or use development by default
  const file = config.env.configFile; //we will use no default value

  return getConfigurationByFile(file);
};
```

- _JSON server configuration_

  - Clone JSON Server
  - run _npm install_
  - run _npm install -g json-server_
  - run _npm run start_

## Key folders & Files

- _cypress.json_ - change default values - This is place where all the deafult settings are placed. Preview - Cypress main screen, third tab - Settings. [Link for documentation]("https://docs.cypress.io/guides/references/configuration#Timeouts")

---

# Mocca and Hooks

Mocca is used to give structure to our automated tests

- _describe()_ - functiion that gruoups test cases

```js
describe("Name of the test group / Description", callback_function() => {});

describe("Description", () => {});
```

- _it()_ - function for individual test case

```js
it("Test case", callback_function() => {})
```

- _it.only()_ - function that executes only selected test from the gruop of tests

- _before()_ - runs once before all tests in the block

- _after()_ - runs once after all tests in the block

- _beforeEach()_ - runs before each test in the block

- _afterEach()_ - runs after each test in the block

---

# Assertions

CHAI - Way of validating wheatger the application is bahaving and presented in a way which we expect.

- _should_
- _expect_
- _assert_
- Chainable words:

  ```jsg
  to, be, been, is, that, which, and, has, have, with, at, of, same
  ```

- _have.prop_, _have.attr_

## should()

- To make an assertion about the current subject, use the .should() command.

- Full [list](https://docs.cypress.io/guides/references/assertions#TDD-Assertions)

```js
// Common assertions
.should('have.class', 'success')
.should('have.text', 'Column content')
.should('contain', 'Column content')
.should('have.html', 'Column content')
.should('match', 'td')
.should('match', /column content/i)
.should('be.visible')
.should('be.disabled')
.should('have.value', '630.00')
.should('have.attr', 'placeholder', 'Email')
.should('be.gt') //be greater than


```

- To assert input elements use have.value
- To assert non-input elements use contain assertion

## and()

- To chain multiple assertions together, use the .and() command.

```js
// Chaining
.should('have.length', 3).and('be.visible')
.should('exist')
  .and('have.length', 3)
  // but should not be visible to the user
  .and('not.be.visible')
```

## expect()

- To make a BDD assertion about a specified subject, use expect.

```js
expect(el).to.have.attr("href", "/about");
expect(el).to.have.attr("target", "_blank");
```

## Chainable getters

-They don't actually do anything, but they enable you to write clear, english sentences.

```json
to, be, been, is, that, which, and, has, have, with, at, of, same
```

# Functions

## Selecting elements

### get()

Get one or more DOM elements by selector or alias

```js
cy.get(selector);
cy.get(alias);
cy.get(selector, options);
cy.get(alias, options);

//  escaping specials characters
<div id="user:1234" class="admin.user">
  Test
</div>;
cy.get("#user\\:1234").should("have.text", "Joe");
cy.get(".admin\\.user");

//  Element starting with TEXT ^=
cy.get("[id^=local-example]").should("have.text", "first");

// Element ending with TEXT $=
cy.get("[id$=example-AF9]").should("have.text", "second");

// Element containing TExY within properties *=
cy.get('a[href*="help"]');

// Get by invoking methods via invoke()
cy.get('[data-test-id="test-example"]')
  .invoke("attr", "data-test-id")
  .should("equal", "test-example");

cy.get('[data-test-id="test-example"]')
  .invoke("css", "position")
  .should("equal", "static");

// Chain assertions
cy.get('[data-test-id="test-example"]')
  .should("have.attr", "data-test-id", "test-example")
  .and("have.css", "position", "static");

// Multiple element get by chaining with comma
cy.get("#and-selector-example p, #and-selector-example li");
```

### contains()

Get the DOM element containing the text. DOM elemets can contain more than the desired text and still match.

```js
.contains(content)
.contains(content, options)
.contains(selector, content)
.contains(selector, content, options)

// ---or---

cy.contains(content)
cy.contains(content, options)
cy.contains(selector, content)
cy.contains(selector, content, options)

{ matchCase: false }

// ignore case
cy.contains(/cypress user/i)
// match text exactly
cy.contains(/^Cypress User$/)


// The text can be anywhere in the element or its children.
```

### within()

Scopes all subsequent cy commands to within this element. Useful when working within a particular group of elements such as a <form>.

```js
.within(callbackFn)
.within(options, callbackFn)

// usage
cy.get('.list').within(($list) => {}) // Yield the `.list` and scope all commands within it

```

## Traversal in JS and Cypress

```js
// children() - to get the children of DOM elements

cy.get(".traversal-breadcrumb")
  .children(".active")
  .should("contain", "Contact Us");

// closest() to validate the closest ancestor DOM element

cy.get(".traversal-badge").closest("ul").should("have.class", "list-group");

//  eq() to retrieve a specific element based on index

cy.get(".traversal-drinks-list > *").eq(2).should("contain", "Milk");

// filter() to retrieve DOM elements that match a specific selector
cy.get(".btn-group-toggle > *").filter(".active").should("contain", "Button-1");

// "find() to retrieve DOM elements of a given selector
cy.get(".traversal-pagination").find("a").should("have.length", 7);

//  first() to retrieve the first DOM element within elements

cy.get(".traversal-table > tbody > tr > td").first().should("contain", "Andy");

//  last() to retrieve the last DOM element within elements

cy.get(".traversal-table > tbody > tr > td").last().should("contain", "Scott");

//  nextAll() to get all of the next sibling DOM elements within elements
cy.get(".traversal-drinks-list")
  .contains("Tea")
  .nextAll()
  .should("have.length", 3);

// nextUntil() to get all of the next sibling DOM elements within elements until another element
cy.get("#coffee").nextUntil("#milk").should("contain", "Tea");

// not() to remove DOM element(s) from the set of elements

cy.get(".traversal-button-states > *")
  .not(".disabled")
  .should("not.have.class", "disabled");

// parent() To get parent DOM element of elements

cy.get(".traversal-mark")
  .parent()
  .should("contain", "Lorem ipsum dolor sit amet, consectetur adipiscing elit");

// parents() to get parents DOM element of elements
cy.get(".traversal-cite").parents().should("match", "blockquote");

// prev() to get the previous sibling DOM element within elements
cy.get("#sugar").prev().contains("Espresso");

// prevAll() to get all previous sibling DOM elements within elements
cy.get(".sales").prevAll().should("have.length", "2");

// prevUntil() to get all previous sibling DOM elements within elements until other element

cy.get("#veggie").prevUntil("#fruits").should("have.length", "5");

// siblings() To get all sibling DOM elements of elements
cy.get(".traversal-button-other-states .active")
  .siblings()
  .should("have.length", 3);
```

## Actions

### type()

- Type into a DOM element

```js
.type(text)
.type(text, options)
```

- We can clear field before typing with _clear()_

### focus(), blur(), clear()

- To focus on a DOM element, use the .focus() command.
- To blur on a DOM element, use the .blur() command.
- To clear on a DOM element, use the .clear() command.

### submit()

- To submit a form, use the cy.submit() command.

### click()

- Click a DOM element

```js
.click()
.click(options)
.click(position)
.click(position, options)
.click(x, y)
.click(x, y, options)
```

```js
// Options:
cy.click({force: true}) - if element is not visible on the page or has set 0x0 w/h force click on it to proceed with test
{ multiple: true } - to click on multiple elements pass this parameter
```

### dblclick(), rightclick()

- To double click a DOM element, use the .dblclick() command.
- To right click a DOM element, use the .rightclick() command.

### check()

- Check checkbox(es) or radios. This element must be an input width type checkbox or radio

```js
.check()
.check(value)
.check(values)
.check(options)
.check(value, options)
.check(values, options)
```

```js
.check('US')
.check(['US','EN'])
```

### uncheck()

- Check checkbox(es) or radios. This element must be an input width type checkbox or radio

```js
.uncheck()
.uncheck(value)
.uncheck(values)
.uncheck(options)
.uncheck(value, options)
.uncheck(values, options)
```

```js
.uncheck('US')
.uncheck(['US','EN'])
```

### select()

- Select an option within a select. We can select via value or via option text

```js
.select()
.select(value)
.select(values)
.select(options)
.select(value, options)
.select(values, options)
```

```js
.select('US')
.select(['US','EN'])
```

### scrollIntoView(), scrollTo()

- To scroll an element into view, use the .scrollintoview() command.
- To scroll the window or a scrollable element to a specific position, use the cy.scrollTo() command.

### trigger

- Trigger and event on a DOM element

```js
.trigger(eventName)
.trigger(eventName, position)
.trigger(eventName, options)
.trigger(eventName, x, y)
.trigger(eventName, position, options)
.trigger(eventName, x, y, options)
```

### Mouse actions - draggable(), droppable()

```js
// drag and drop which1 - deprecated but means that it will click in center of element

cy.get("#draggable").trigger("mousedown", {
  which: 1,
});

cy.get("#droppable").trigger("mousemove").trigger("mouseup", {
  force: true,
});
```

## Location

### hash()

- To get the current URL hash, use the cy.hash() command.

### location()

- To get window.location, use the cy.location() command.

### url()

- To get the current URL, use the cy.url() command

## Navigation

### go('forward'), go('back'), go(-1), go(1)

- To go back or forward in the browser's history, use the cy.go() command.

### reload()

- To reload the page, use the cy.reload() command.

### visit()

- Visit a remote URL

```js
cy.visit("BASE URL");
```

## Window

### window()

- To get the global window object, use the cy.window() command.

### document()

- To get the document object, use the cy.document() command.

### title()

- To get the title, use the cy.title() command.

## Misc

### log()

- Print a message to the Cypress Command Log

```js
cy.log(message); // Gets current URL as a string
cy.log(message, args, ...);
```

### end()

- To end the command chain, use the .end() command.
- cy.end is useful when you want to end a chain of commands

### exec()

- To execute a system command, use the cy.exec() command.

### focused()

- To get the DOM element that has focus, use the cy.focused() command.

### screenshot()

- To take a screenshot, use the cy.screenshot() command.

### wrap()

- Yield the object passed into .wrap() . If the object is a promise, yield its resolved value
- Once you have an object wrapped, you can access its properties, invoke its methods, and even pass it via an alias.

```js
cy.wrap(subject);
cy.wrap(subject, options);
```

### pause()

- Stop cy commands from running and allow interaction with the application under test. You can then "resume" running all commands or choose to step through the "next" commands from the Command Log.

```js
.pause()
.pause(options)

cy.pause()
cy.pause(options)

```

```js
// usage:
cy.pause().getCookie("app"); // Pause at the beginning of commands
cy.get("nav").pause(); // Pause after the 'get' commands yield
```

### wait()

- Wait for a number of milliseconds or wait for an aliased resource to resolve before moving on to the next command.

```js
cy.wait(time);
cy.wait(alias);
cy.wait(aliases);
cy.wait(time, options);
cy.wait(alias, options);
cy.wait(aliases, options);
```

```js
// usage
cy.wait(500);
cy.wait("@getProfile");
```

### eq

- Get a DOM element at a specific index in an array of elements

```js
.eq(index)
.eq(indexFromEnd)
.eq(index, options)
.eq(indexFromEnd, options)

```

### Cookies and Local Storage

```js
cy.getCookie();
cy.getCookies();
cy.setCookie();
cy.clearCookie();
cy.clearCookies();
```

- You can directly access the browser's localStorage object.

```js
localStorage.getItem("AppSays");
localStorage.setItem("prop1", "red");
localStorage.setItem("prop2", "blue");
localStorage.setItem("prop3", "magenta");
```

## Connectors

### each()

- Iterate through an array like structure(arrays or objects with a length property)

```js
.each(callbackFn);

cy.get("SELECTOR").each(($el, index, $list) => {

})
```

### its()

-To get the properties on the current subject, use the .its() command. For example, if the subject is the list of found elements, we can grab its length property and use it in the assertion:

### then()

- Enables you to work with the subject yieded from the previous command. Controls what is the order of executing and displaying

```js
.then(callbackFn); // Gets current URL as a string
.then(options, callbackFn);
```

### invoke()

- Invoking JQuery and JS methods and funnctions

```js
cy.get(".modal").invoke("show");
```

### spread()

- To spread an array as individual arguments to a callback function, use the .spread() command.

```js
const arr = ["foo", "bar", "baz"];

cy.wrap(arr).spread(function (foo, bar, baz) {
  expect(foo).to.eq("foo");
  expect(bar).to.eq("bar");
  expect(baz).to.eq("baz");
});
```

## Files

### fixtures()

- Load a fixed set of data located in a file

```js
cy.fixture(filePath);
cy.fixture(filePath, encoding);
cy.fixture(filePath, options);
cy.fixture(filePath, encoding, options);

// fixture initialization
cy.fixture("example.json").then(function (data) {
  // this.data = data
  globalThis.data = data;
});

//  data is accessed by typing:
data.NAME_FROM_JSON_FILE;
```

### readFile(), writeFile()

- To read a file's content, use the cy.readFile() command.
- To write to a file with the specified contents, use the cy.writeFile() command.

## Network Requests

### request()

```js
cy.request(url);
cy.request(url, body);
cy.request(method, url);
cy.request(method, url, body);
cy.request(options);

// Usage

cy.request("POST", "https://jsonplaceholder.cypress.io/posts", {
  userId: user.id,
  title: "Cypress Test Runner",
  body: "Fast, easy and reliable testing for anything that runs in a browser.",
});

cy.request({
  method: "DELETE / PUT / POST / GET",
  url: "localhost:3000/posts/12",
  body: {
    // "title": "Do you want to learn automation testing",
    title: "Updated title - Test",
    author: "Nikolina Nina Ina Test Update PUT method",
  },
  headers: {
    accept: "application/json", // ONLY FOR GET REQUEST
  },
}).then((response) => {
  expect(response.status).to.equal(200);
});
```

### intercept()

Spy and stub network requests and responses.

```js
cy.intercept(url);
cy.intercept(method, url);
cy.intercept(routeMatcher);

// spying and response stubbing
cy.intercept(url, staticResponse);
cy.intercept(method, url, staticResponse);
cy.intercept(routeMatcher, staticResponse);
cy.intercept(url, routeMatcher, staticResponse);

// spying, dynamic stubbing, request modification, etc.
cy.intercept(url, routeHandler);
cy.intercept(method, url, routeHandler);
cy.intercept(routeMatcher, routeHandler);
cy.intercept(url, routeMatcher, routeHandler);

// Usage
// https://on.cypress.io/intercept

let message = "whoa, this comment does not exist";

// Listen to POST to comments
cy.intercept("POST", "**/comments").as("postComment");

// we have code that posts a comment when
// the button is clicked in scripts.js
cy.get(".network-post").click();
cy.wait("@postComment").should(({ request, response }) => {
  expect(request.body).to.include("email");
  expect(request.headers).to.have.property("content-type");
  expect(response && response.body).to.have.property(
    "name",
    "Using POST in cy.intercept()"
  );
});

// Stub a response to PUT comments/ ****
cy.intercept(
  {
    method: "PUT",
    url: "**/comments/*",
  },
  {
    statusCode: 404,
    body: { error: message },
    headers: { "access-control-allow-origin": "*" },
    delayMs: 500,
  }
).as("putComment");

// we have code that puts a comment when
// the button is clicked in scripts.js
cy.get(".network-put").click();

cy.wait("@putComment");

// our 404 statusCode logic in scripts.js executed
cy.get(".network-put-comment").should("contain", message);

// we can spy on requests that do not have a response body
cy.intercept("DELETE", "/comments/1").as("delete");
cy.get(".network-delete").click();
cy.wait("@delete");
cy.contains(".network-delete-comment", "Comment deleted!");
```

### XHR Testing

XHR is an API in teh form of an object whose methods transfer data brtween a web browser an a web server. Cypress provides direct access to XHR objets, enabling us to create assertions based upon the properties of the XHR objects. We can alsu stub and mock the response of an XHR object

1. Disable XHR displaying / support/index.js - from version 5.0.

```js
Cypress.Server.defaults({
  ignore: (xhr) => true,
});

// OLD CODE for v4.12.1. DEPRECATED
Cypress.Server.defaults({
  whitelist: (xhr) => {
    return true;
  },
});
```

---

# Aliasing

- Sharing context is the simplest way to use Aliases. To alias something you would like to share we use _as()_ command.
- Aliases are available as \*this.\*\*
- When we call aliases we use @ sign

```js
// Example
cy.get(".as-table")
  .find("tbody>tr")
  .first()
  .find("td")
  .first()
  .find("button")
  .as("firstBtn");

// when we reference the alias, we place an
// @ in front of its name
cy.get("@firstBtn").click();

cy.get("@firstBtn")
  .should("have.class", "btn-success")
  .and("contain", "Changed");
```

# Selectors

- Select by name : [name = "name"]
- Select by type : [type = "type"]
- XPATH selectors

  - nodename - All nodes with the name "nodename"
  - / - Selects from the root node
  - // - Selects nodes in teh documents from the current node that match the selection no matter where they are
  - . - Selects the current node
  - .. - Selects the parent of the current node
  - @ - Selects attributes
  - \* wild card
  - $ - look at the end of whatever we search for
  - ^ - starts with

  ```js
  //By tag name
  cy.get("input");

  //By attribute name and value
  cy.get("input[name='first_name']");

  //By id
  cy.get("#contact_me");

  //By class
  cy.get(".feedback-input");

  //By multiple classes
  cy.get("[class='navbar navbar-inverse navbar-fixed-top']");

  //By two different attributes
  cy.get("[name='email'][placeholder='Email Address']");

  //By xpath
  cy.xpath("//input[@name='first_name']");
  ```

---

# Plugins

## cypress XPath

```js
npm install -D cypress-xpath
// Then include in projects cypress/support/index.js
require('cypress-xpath)
```

## Cypress RETRIABILITY- Commes preinstalled in Cypress v5

```js
// npm install -D cypress-plugin-retries DEPRECATED
// At the top og cypress/support/index.js DEPRECATED
// require('cypress-plugin-retries') DEPRECATED
// In cypress.json in env
// "RETRIES": 2, - DEPRECATED
// Directly in test
// Cypress.currentTest.retries(4) - DEPRECATED


// in cypress.json
"retries": {
      "runMode": 1,
      "openMode": 2
    }
// in test definition : TO override default settings in cypress.json

it("Description", {
retries:{
  runMode: 2,
  openMode: 2
}
}, () => {

})

// VIA NPX

CYPRESS_RETRIES=1 npm run NAMEOFSCRIPT
```

- _runMode_ - Allows zou to deine the number of test retries when running cypress run

- _openMode_ - Allows zou to deine the number of test retries when running cypress open

## Cucumber preprocessor - Run cucumber/gherkin szntax with Cypress.io

```js
npm install --save-dev cypress-cucumber-preprocessor

//  in cypress/plugins/index.js

const cucumber = require('cypress-cucumber-preprocessor').default

module.exports = (on, config) => {
  on('file:preprocessor', cucumber())
}

// in package.json
 "cypress-cucumber-preprocessor": {
    "nonGlobalStepDefinitions": true
  },

```

---

# Tips and Tricks

## Multiple tabs tricks

```js
// REMOVE target="_blank"

cy.get("#contact-us").invoke("removeAttr", "target").click({
  force: true,
});

//
```

## Same origin trick

```js
// set chromeWebSecurity to false in cypress.json
{
  "chromeWebSecurity": false
}
//
```

---

## Handling JS events / Alerts

When handling JS events we use .on function

```js
cy.on("window:alert", (str) => {
  expect(str).to.equal("I am an alert box!");
});
```

When handling alerts automatically we use _window:alert_ - We cannot chanfge behaviour of clicking ok

When we need to Click Cancel or control alerts we use _window:confirm_

- Handling JS Alerts with stubs

```js
// Replace a function, record its usage and control its behavior
const stub = cy.stub();
cy.on("window:confirm", stub);

cy.get("#button4")
  .click()
  .then(() => {
    expect(stub.getCall(0)).to.be.calledWith("Press a button!");
  })
  .then(() => {
    return true;
  })
  .then(() => {
    cy.get("#confirm-alert-text").contains("You pressed OK!");
  });
```

## Handling iframes

If website uses iframe that is a cross-origin frame, Cypress will not be able to automate or communicate with this iframe.

```js
// How to make Cypress use iframe
cy.get("#frame").then(($iframe) => {
  const body = $iframe.contents().find("body");
  cy.wrap(body).as("iframe");
});
// How to interact with iframe
```

---

## Environment Variables Options

Any key/value you set in your configuration file (cypress.json by default) under the env key will become an environment variable.

```json
{
  "projectId": "128076ed-9868-4e98-9cef-98dd8b705d75",
  "env": {
    "login_url": "/login",
    "products_url": "/products"
  }
}
```

In test file:

```js
Cypress.env(); // {login_url: '/login', products_url: '/products'}
Cypress.env("login_url"); // '/login'
Cypress.env("products_url"); // '/products'
```

Alter env in runtime

```json
./node_modules/.bin/cypress run --browser electron --spec cypress/integration/webdriver-uni/contact-us.js --env first_name=Nina
```

## Global options

```json
// Simple URL
"baseUrl": "LINK"
```

```js
cy.visit("/"); //goes to Base URL
```

## Custom - Cypress.Commands.add()

You define custom command in support/commands.js and call it as a function

```js
Cypress.Commands.add(name, callbackFn);
Cypress.Commands.add(name, options, callbackFn);
Cypress.Commands.overwrite(name, callbackFn);
```

## Handling File upload

```js
// Install dependences first, place image in fixtures folder

cy.fixture("user.jpg", "base64").then((fileContent) => {
  cy.get("#myFile").attachFile(
    {
      fileContent,
      fileName: "user.jpg",
      mimeType: "image/jpg",
    },
    {
      uploadType: "input",
    }
  );
});
```

## Configuring Viewports

Control the size and orientation of the screen for your application. You can set the viewport's width and height globally by defining viewportWidth and viewportHeight in the configuration. [Presets link](https://docs.cypress.io/api/commands/viewport#Arguments)

```js
cy.viewport(width, height);
cy.viewport(preset, orientation);
cy.viewport(width, height, options);
cy.viewport(preset, orientation, options);

// USAGE:
cy.viewport(550, 750); // Set viewport to 550px x 750px
cy.viewport("iphone-6"); // Set viewport to 375px x 667px
```

# Scripts and configurations

## Making script in package.json

By making script we shorten the time we spend to type whole commands and whole paths. We use it after we installed npx package.

```json
 "scripts": {
     "triggerAllTests-headless": "npx cypress run",
    "triggerAllTests-headed": "npx cypress run --headed",
    "triggerAllTests-chrome": "npx cypress run --browser chrome",
    "triggerAllTests-dashboard": "npx cypress run --record --key 2d371a28-26bf-4095-89a8-29db87b4860d ",
    "triggerAllTests-webdriveruni": "npx cypress run --spec cypress/integration/webdriver-uni/*",
    "triggerAllTests-automationteststore": "npx cypress run --spec cypress/integration/automation-test-store/*",
    "junit-merge": "npx junit-merge -d cypress/results/junit -o cypress/results/junit/results.xml",
    "junit-delete": "rm -rf cypress/results/junit/results.xml",
    "delete-results": "rm -rf cypress/results/* || true",
    "mochawesome-merge": "npx mochawesome-merge cypress/results/mochawesome/*.json > mochawesome.json && npx marge mochawesome.json",
    "mochawesome-delete": "rm -rf mochawesome-report/* || true",
    "cypress-regression-rack": "npm run detele-results && npm run mochawesome-delete && npm run triggerAllTests-headless && npm run mochawesome-merge",
    "triggerAllTests-staging": "npx cypress run --enc configFile=staging"

  }

  //  We call it in terminal via npm run NAME_OF_SCRIPT
```

## Different configurations

```json
{
  "baseUrl": "http://www.webdriveruniversity.com/",
  "chromeWebSecurity": false,
  "defaultCommandTimeout": 10000,
  "pageLoadTimeout": 30000,
  "viewportHeight": 1080,
  "viewportWidth": 1920,
  "ignoreTestFiles": "same*.js",
  "screenshotsFolder": "cypress/screenshots",
  "retries": {
    "runMode": 0,
    "openMode": 0
  },
  "env": {
    "webdriveruni_homepage": "http://www.webdriveruniversity.com/",
    "first_name": "sarah"
  },
  "projectId": "5rkxf9",
  "reporter": "cypress-multi-reporters",
  "reporterOptions": {
    "configFile": "reporter-config.json"
  }
}
```

# Reporting

- _npm install --save-dev cypress-multi-reporters mocha-junit-reporter_ - Install dependencies for reporting - Mocha JUnit Reports

- _npx junit-merge -d cypress/results/junit -o cypress/results/junit/results.xml_ Merge JUnit reports into one

- _npm install --save-dev mochawesome mochawesome-merge mochawesome-report-generator_ - Install Mochawesome and its dependencies

- _npx mochawesome-merge cypress/results/mochawesome/\*.json > mochawesome.json && npx marge mochawesome.json_ Merge all mochawesome reports in one and generate HTML report in that one file

```js
// After that we need to add the separate reporter-config.json file to enable spec and junit and direct the junit reporter to save separate XML files

// In config file - cypress.js we put
{
  "reporter": "cypress-multi-reporters",
  "reporterOptions": {
    "configFile": "reporter-config.json"
  }
}

// We make new file in the root of project and put this (JUNIT + MOCHAWESOME)
{
    "reporterEnabled": "spec, cypress-multi-reporters",
    "mochaJunitReporterReporterOptions": {
      "mochaFile": "cypress/results/junit/results-[hash].xml"
    },
    "reporterOptions": {
      "reporterEnabled": "mochawesome",
      "mochawesomeReporterOptions": {
        "reportDir": "cypress/results/mochawesome",
        "quite": true,
        "overwrite": false,
        "html": false,
        "json": true

      }
    }
}

```

# Best Practices

## Selecting element

- Prefer dedicated data-cy or data-test attributes to CSS class names and element IDs.

## _cy.get_ vs _cy.find_

- The _cy.get_ command always starts its search from the document element, or, if used inside .within, from the cy.root element. The _.find_ command starts the search from the current subject.
