---
sidebar_position: 3
---

# Set Up & Teardown

In automated testing, it's often necessary to set up some global state before tests run and clean up afterwards. This process is known as "setup" and "teardown." Jest provides several methods to handle setup and teardown, ensuring your tests run in a controlled environment. Understanding how to use these methods allows you to write more reliable and maintainable tests.

## Basic Setup and Teardown

Jest offers simple methods for basic setup and teardown scenarios:

- `beforeEach` and `afterEach`: Run some code before and after each test in a test file.
- `beforeAll` and `afterAll`: Run some code once before and after all the tests in a test file.

### Using `beforeEach` and `afterEach`

These are useful for setting up a fresh environment for each test, which helps prevent tests from affecting each other.

```javascript
describe("using beforeEach and afterEach", () => {
  beforeEach(() => {
    // Initialize or reset the test environment before each test.
  });

  afterEach(() => {
    // Clean up the test environment after each test.
  });

  test("test 1", () => {
    // Test code here
  });

  test("test 2", () => {
    // Test code here
  });
});
```

### Using `beforeAll` and `afterAll`

These methods are suitable for performing setup and teardown operations that only need to happen once for the entire suite of tests, such as initializing a database connection or clearing a cache.

```javascript
describe("using beforeAll and afterAll", () => {
  beforeAll(() => {
    // Run some code once before all tests start.
  });

  afterAll(() => {
    // Run some code once after all tests finish.
  });

  test("test 1", () => {
    // Test code here
  });

  test("test 2", () => {
    // Test code here
  });
});
```

## Scoping

Setup and teardown methods can be scoped to describe blocks. This means you can have setup and teardown apply to all tests within a `describe` block, allowing for more granular control over the test environment.

```javascript
// Applies to all tests in the file
beforeEach(() => {
  // Global setup
});

describe("group 1", () => {
  // Applies only to tests within this describe block
  beforeEach(() => {
    // Group 1 setup
  });

  test("test 1", () => {
    // Test code here
  });
});

describe("group 2", () => {
  // Applies only to tests within this describe block
  beforeEach(() => {
    // Group 2 setup
  });

  test("test 2", () => {
    // Test code here
  });
});
```

## Async Setup and Teardown

Jest supports asynchronous setup and teardown operations, which is useful when you need to perform async operations like API calls or database operations before or after your tests.

You can return a promise from your setup/teardown functions, or use async/await syntax:

```javascript
beforeAll(async () => {
  await database.connect();
});

afterAll(async () => {
  await database.disconnect();
});
```

## Conclusion

Properly using setup and teardown methods in Jest can greatly enhance your testing experience, making your tests more reliable and easier to read and maintain. By preparing the environment before tests run and cleaning up afterwards, you ensure that tests do not interfere with each other and that resources are properly managed.
