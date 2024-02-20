---
sidebar_position: 1
---

# Test Suites & Test Cases

In Jest, tests are organized into test suites and test cases. This structure helps in managing and categorizing tests, making it easier to understand what each test does and to identify which parts of your application are tested. Below, we delve into what test suites and test cases are, and how they are used in Jest.

## Test Suites

A test suite is a collection of test cases that are related to each other. This grouping helps in organizing tests logically, usually by application feature or functionality. In Jest, a test suite is typically defined by a file containing one or more test cases.

### Creating a Test Suite

In Jest, each file with tests is considered a test suite. For example, if you have a file named `sum.test.js`, it represents a test suite for the `sum` functionality in your application.

## Test Cases

A test case is a single unit test. It represents an individual test of a specific functionality or part of your application. Test cases are defined using the `test` or `it` functions in Jest, and they contain the actual testing code.

### Writing a Test Case

Here's how you can write a simple test case using the `test` function:

```javascript
test("adds 1 + 2 to equal 3", () => {
  const sum = require("./sum");
  expect(sum(1, 2)).toBe(3);
});
```

In this example, the test case checks if the `sum` function correctly adds the numbers 1 and 2 to equal 3.

### Using `it` Instead of `test`

You can also use `it` instead of `test` to define a test case. Both are aliases and work the same way; the choice between them is purely stylistic and can depend on your or your team's preference for readability. Here's how the same test case would look using `it`:

```javascript
it("adds 1 + 2 to equal 3", () => {
  const sum = require("./sum");
  expect(sum(1, 2)).toBe(3);
});
```

## Grouping Test Cases with `describe`

For even better organization, especially in complex applications, Jest provides the `describe` function to group related test cases into a sub-section within a test suite. This is particularly useful for grouping tests by functionality or component.

### Example of Using `describe`

```javascript
describe("sum module", () => {
  test("adds 1 + 2 to equal 3", () => {
    const sum = require("./sum");
    expect(sum(1, 2)).toBe(3);
  });

  // More tests related to the sum module
});
```

In this example, `describe` is used to group all test cases related to the `sum` module. You can nest `describe` blocks to create sub-groups for even more granular organization.

## Practical Example

Let's consider a simple module that performs operations on an array of numbers: it can add a number to the array, find the average of the numbers, and check if all elements are even. We'll implement this module and then create a full test suite for it using Jest.

### Step 1: Implementation of the Module

First, let's write the implementation of our module, `NumberArrayOperations.js`:

```javascript
class NumberArrayOperations {
  constructor() {
    this.numbers = [];
  }

  addNumber(number) {
    this.numbers.push(number);
  }

  getAverage() {
    const sum = this.numbers.reduce((acc, curr) => acc + curr, 0);
    return sum / this.numbers.length || 0;
  }

  areAllEven() {
    return this.numbers.every((num) => num % 2 === 0);
  }
}

module.exports = NumberArrayOperations;
```

### Step 2: Creating the Test Suite

Now, let's create a test suite for this module in a file named `NumberArrayOperations.test.js`.

```javascript
const NumberArrayOperations = require("./NumberArrayOperations");

describe("NumberArrayOperations", () => {
  let operations;

  beforeEach(() => {
    operations = new NumberArrayOperations();
  });

  test("initially has an empty array", () => {
    expect(operations.numbers).toEqual([]);
  });

  test("adds a number to the array", () => {
    operations.addNumber(5);
    expect(operations.numbers).toContain(5);
  });

  test("calculates the average of the numbers", () => {
    operations.addNumber(4);
    operations.addNumber(6);
    expect(operations.getAverage()).toBe(5);
  });

  test("returns 0 for average when array is empty", () => {
    expect(operations.getAverage()).toBe(0);
  });

  test("checks if all numbers are even", () => {
    operations.addNumber(2);
    operations.addNumber(4);
    expect(operations.areAllEven()).toBeTruthy();
  });

  test("returns false if not all numbers are even", () => {
    operations.addNumber(1);
    operations.addNumber(2);
    expect(operations.areAllEven()).toBeFalsy();
  });
});
```

### Step 3: Running the Tests

Ensure you have Jest installed in your project. If not, install it by running:

```bash
npm install --save-dev jest
```

Add a test script to your `package.json`:

```json
"scripts": {
  "test": "jest"
}
```

Now, run the tests using npm:

```bash
npm test
```

This test suite covers the functionality of our `NumberArrayOperations` class by checking:

- The initial state of the numbers array.
- The ability to add a number to the array.
- The calculation of the average from the numbers array.
- The behavior of the average calculation when the array is empty.
- Whether all numbers in the array are even.

Each test initializes a fresh instance of `NumberArrayOperations` to ensure tests do not affect each other, following best practices for unit testing. This suite helps ensure that our module behaves as expected under various conditions.

## Conclusion

Understanding and effectively using test suites and test cases are fundamental in structuring your tests in Jest. This organization not only makes your tests easier to manage and maintain but also improves readability and the overall development experience. By grouping related tests using `describe` and defining individual tests with `test` or `it`, you can create a comprehensive and organized test suite for your application.
