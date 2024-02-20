---
sidebar_position: 4
---

# Mock Functions & Modules

Jest provides extensive support for mocking functions and modules, enabling more effective and isolated unit tests. Mocks can help in testing modules in isolation by replacing dependencies or other external calls with mock implementations that mimic real behavior without executing actual logic.

## Mock Functions

Mock functions, also known as "spies," are used to track calls to a function and mock its implementation. They can be created using `jest.fn()` and have several uses:

### Tracking Calls

You can track how, when, and how many times a mock function is called. This is useful for ensuring that your functions are called correctly.

```javascript
const mockFunction = jest.fn();

mockFunction();
mockFunction("hello");

test("function has been called twice", () => {
  expect(mockFunction.mock.calls.length).toBe(2);
});

test('second call was called with "hello"', () => {
  expect(mockFunction.mock.calls[1][0]).toBe("hello");
});
```

### Mocking Return Values

Mock functions can be configured to return specific values.

```javascript
const mock = jest.fn(() => true);

test("mock function returns true", () => {
  expect(mock()).toBe(true);
});
```

### Implementing Custom Behavior

You can also provide a custom implementation for a mock function.

```javascript
const mock = jest.fn().mockImplementation((a, b) => a + b);

test("mock implementation of add", () => {
  expect(mock(1, 2)).toBe(3);
});
```

## Mock Modules

Jest allows you to mock entire modules, which is particularly useful when you want to test modules in isolation without relying on their real implementations, such as API clients or database modules.

### Automatic Mocks with `jest.mock`

You can automatically mock a module using `jest.mock('moduleName')`.

```javascript
// Automatically mock the axios module
jest.mock("axios");

const axios = require("axios");
const fetchData = () => axios.get("/data");

test("fetches data", () => {
  axios.get.mockResolvedValue({ data: "some data" });

  fetchData().then((data) => {
    expect(data).toEqual({ data: "some data" });
  });
});
```

### Manual Mocks

For more control, you can create manual mocks by adding a file in a `__mocks__` directory adjacent to the module. Jest will use the mock implementation from this file instead of the node module.

For example, to mock a module named `apiClient`, you would create a file at `__mocks__/apiClient.js` with your mock implementation.

## Using Mocks for Dependency Injection

Mocks are particularly useful for dependency injection, where a module's dependencies are replaced with mocks. This allows you to test the module's functionality independently of its external dependencies.

```javascript
// apiClient.js is a dependency of myModule.js
jest.mock("./apiClient"); // Mock apiClient

const myModule = require("./myModule");
const apiClient = require("./apiClient");

apiClient.getData.mockResolvedValue("mock data");

test("myModule calls apiClient and returns data", async () => {
  const data = await myModule.getData();
  expect(data).toBe("mock data");
});
```

## Conclusion

Mocking functions and modules with Jest is a powerful way to build isolated and deterministic tests. By controlling the behavior of dependencies and tracking calls to functions, you can ensure your tests focus on the code under test and behave consistently across test runs.
