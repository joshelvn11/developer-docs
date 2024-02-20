---
sidebar_position: 5
---

# Mocking The DOM

DOM (Document Object Model) mocking and testing are essential parts of front-end development, enabling developers to test interactions with the web page as if they were running in a real browser environment. Jest, combined with utilities like `@testing-library/react` for React components or similar libraries for other frameworks, provides a powerful environment for testing DOM manipulations and user interactions. This explanation will focus on general concepts applicable across various frameworks and libraries.

## Why Mock the DOM?

In unit and integration tests, you often need to simulate the behavior of web page elements without running the tests in a browser. Mocking the DOM allows you to:

- Test components in isolation from the rest of the web page or application.
- Simulate user actions (clicks, input, navigation) and test the resulting changes in the DOM.
- Test the lifecycle of web components, including creation, update, and destruction.
- Ensure your application behaves correctly in various scenarios, including form submissions and asynchronous data fetching.

## Setting Up Jest for DOM Testing

Jest runs in a Node.js environment and doesn't have access to the browser's DOM. However, Jest provides a simulated DOM using [jsdom](https://github.com/jsdom/jsdom), a pure-JavaScript implementation of many web standards, out of the box.

For most use cases, Jest's default jsdom environment is sufficient to simulate browser-like behavior. However, you might sometimes need to customize the jsdom environment for specific tests. You can do this in your Jest configuration file (`jest.config.js`) or directly in your test files.

## Basic DOM Mocking and Testing

Here's a simple example of how to test DOM interactions using Jest:

```javascript
document.body.innerHTML = `
  <div>
    <span id="username"></span>
    <button id="button">Click me</button>
  </div>
`;

const button = document.querySelector("#button");
const username = document.querySelector("#username");

button.addEventListener("click", () => {
  username.textContent = "John Doe";
});

test('username should be "John Doe" after button click', () => {
  // Simulate button click
  button.click();

  // Assert that username's textContent changed appropriately
  expect(username.textContent).toBe("John Doe");
});
```

In this example, we set up a simple HTML structure and simulate a user interaction (a button click) that updates the text content of a span. Then, we assert that the expected change occurred.

## Advanced DOM Testing Scenarios

For more complex DOM interactions or when testing components from libraries like React, Vue, or Angular, you'll need additional tools designed for those frameworks. For example, React developers commonly use [@testing-library/react](https://testing-library.com/docs/react-testing-library/intro/) for testing components:

```javascript
import { render, fireEvent } from "@testing-library/react";
import MyComponent from "./MyComponent";

test("it renders and responds to user input", () => {
  const { getByText, getByLabelText } = render(<MyComponent />);

  // Assert that the component renders correctly
  expect(getByText("Submit")).toBeInTheDocument();

  // Simulate user typing in an input field
  fireEvent.change(getByLabelText("Name"), { target: { value: "John Doe" } });

  // Simulate form submission
  fireEvent.click(getByText("Submit"));

  // Assert that the expected behavior occurred
});
```

## Loading The DOM from a File

Loading HTML from an HTML file and attaching it to the mock DOM is a technique used in testing environments, particularly when working with Jest and jsdom. This approach allows you to work with realistic DOM structures without manually defining them in your JavaScript test files, leading to cleaner, more maintainable tests. Here's a detailed explanation of how to achieve this.

### Why Load HTML from an HTML File?

- **Realism**: Use actual HTML structures that your JavaScript interacts with, increasing the realism of your tests.
- **Maintainability**: Keeps your HTML and JavaScript code separate, making both easier to manage and update.
- **Reusability**: Allows you to use the same HTML setup across multiple test cases or suites.

### Step-by-Step Guide

#### 1. Prepare Your HTML File

First, create an HTML file that contains the markup you want to test. For example, `testPage.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Test Page</title>
  </head>
  <body>
    <div id="app"></div>
    <!-- More HTML content here -->
  </body>
</html>
```

#### 2. Load HTML Content in Your Test

To load and use this HTML content in your Jest test, you'll need to read the file from the filesystem and then insert its contents into jsdom's mock DOM. Here's how you can do it:

```javascript
const fs = require("fs");
const path = require("path");

describe("DOM Manipulation Tests", () => {
  beforeAll(() => {
    // Load the HTML file before all tests
    const html = fs.readFileSync(
      path.resolve(__dirname, "testPage.html"),
      "utf8"
    );
    document.documentElement.innerHTML = html;
  });

  test("Example test", () => {
    // Your testing logic here, e.g., checking if the #app div exists
    expect(document.getElementById("app")).not.toBeNull();
  });
});
```

### Tips for Effective Use

- **Relative Paths**: Use relative paths carefully, especially if your tests are running in environments where the current working directory might differ from what you expect. The `__dirname` global in Node.js is helpful for constructing absolute paths.
- **Test Data Separation**: Keep your test-specific HTML files in a separate directory (e.g., `__tests__/html`) to maintain a clear distinction between your application's actual HTML and the markup used for testing.
- **Cleanup**: In tests where the DOM state might affect subsequent tests, consider cleaning up or reloading the HTML in an `afterEach` or `afterAll` block to ensure test isolation.

### Conclusion

Loading HTML from files into the mock DOM in Jest tests allows for more realistic and maintainable testing scenarios when working with web applications. By separating your HTML structures into distinct files and loading them as needed for your tests, you can ensure that your JavaScript logic works as expected in environments that closely mimic real-world use cases.

## Tips for Effective DOM Testing

- **Isolation**: Test components in isolation as much as possible. Use mocks for external dependencies and child components not under test.
- **User-centric**: Focus on testing the user interface from the perspective of user actions and experiences, rather than internal implementation details.
- **Coverage**: Aim for a balance between thorough coverage and test maintainability. It's crucial to test common and critical paths through the interface but avoid overly detailed tests that are brittle and hard to maintain.
- **Asynchronous Behavior**: Pay special attention to asynchronous operations like API calls or delayed updates. Use Jest's async testing capabilities to handle these cases.

## Practical Examples

Let's go through three practical examples of basic DOM mocking and testing using plain JavaScript and Jest. These examples will cover different aspects of DOM interactions such as manipulating text content, handling input fields, and responding to click events.

### Example 1: Testing Text Content Change

This example demonstrates how to test changing the text content of an element in response to an event (e.g., a button click).

#### HTML Setup

```html
<button id="changeTextButton">Change Text</button>
<div id="textContainer">Original Text</div>
```

#### JavaScript

```javascript
document.getElementById("changeTextButton").addEventListener("click", () => {
  document.getElementById("textContainer").textContent = "Updated Text";
});
```

#### Test

```javascript
test("changes text content on button click", () => {
  document.body.innerHTML = `
    <button id="changeTextButton">Change Text</button>
    <div id="textContainer">Original Text</div>
  `;

  require("./yourScript"); // Adjust the path to where your JS code lives

  const button = document.getElementById("changeTextButton");
  button.click();

  expect(document.getElementById("textContainer").textContent).toBe(
    "Updated Text"
  );
});
```

### Example 2: Testing Form Input and Submission

This example shows how to test user input in a form field and the form's submission event, which updates a message on the page.

#### HTML Setup

```html
<form id="form">
  <input id="nameInput" type="text" />
  <button type="submit">Submit</button>
</form>
<div id="greetingMessage"></div>
```

#### JavaScript

```javascript
document.getElementById("form").addEventListener("submit", (e) => {
  e.preventDefault();
  const name = document.getElementById("nameInput").value;
  document.getElementById("greetingMessage").textContent = `Hello, ${name}!`;
});
```

#### Test

```javascript
test("updates greeting message on form submission", () => {
  document.body.innerHTML = `
    <form id="form">
      <input id="nameInput" type="text" />
      <button type="submit">Submit</button>
    </form>
    <div id="greetingMessage"></div>
  `;

  require("./yourScript"); // Adjust the path to where your JS code lives

  const form = document.getElementById("form");
  document.getElementById("nameInput").value = "John Doe";
  form.dispatchEvent(new Event("submit"));

  expect(document.getElementById("greetingMessage").textContent).toBe(
    "Hello, John Doe!"
  );
});
```

### Example 3: Testing Visibility Toggle

This final example tests the toggling of an element's visibility (e.g., showing/hiding a password field).

#### HTML Setup

```html
<input id="passwordInput" type="password" />
<button id="toggleVisibility">Show/Hide</button>
```

#### JavaScript

```javascript
document.getElementById("toggleVisibility").addEventListener("click", () => {
  const passwordInput = document.getElementById("passwordInput");
  if (passwordInput.type === "password") {
    passwordInput.type = "text";
  } else {
    passwordInput.type = "password";
  }
});
```

#### Test

```javascript
test("toggles password input visibility on button click", () => {
  document.body.innerHTML = `
    <input id="passwordInput" type="password" />
    <button id="toggleVisibility">Show/Hide</button>
  `;

  require("./yourScript"); // Adjust the path to where your JS code lives

  const button = document.getElementById("toggleVisibility");
  button.click();

  expect(document.getElementById("passwordInput").type).toBe("text");

  button.click();

  expect(document.getElementById("passwordInput").type).toBe("password");
});
```

These examples illustrate basic DOM manipulation and event handling tests, simulating user interactions and verifying the expected outcomes. Remember to adjust the paths and possibly the environment setup based on your project structure and the specific technologies you're using.

### Conclusion

DOM mocking and testing with Jest allow developers to simulate and assert interactions with the web page in a controlled testing environment. By combining Jest with appropriate utilities and libraries for your framework, you can thoroughly test your application's front-end logic, ensuring it behaves correctly under a wide range of conditions and user actions.
