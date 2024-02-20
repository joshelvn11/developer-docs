---
sidebar_position: 2
---

# Writing Your First Test

Testing is a critical part of software development that helps ensure your code works as expected. Jest, a delightful JavaScript testing framework, makes writing tests easy and enjoyable. In this guide, we'll walk through the process of writing your first test using Jest.

## Step 1: Setting Up Your Project

Before writing tests, ensure that Jest is installed and set up in your project. If you haven't installed Jest yet, you can add it by running:

```bash
npm install --save-dev jest
```

For more detailed installation instructions, refer to the [installation and setup guide](#installation-and-setup).

## Step 2: Writing a Simple Function to Test

To demonstrate how to write a test, we'll create a simple function that adds two numbers. Create a new file named `sum.js` in your project and add the following code:

```javascript
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

This function takes two arguments, `a` and `b`, adds them together, and returns the result.

`module.exports = sum;` makes the sum function available to be imported into other files using require. In this specific case, it allows the sum.test.js file to import the sum function so it can be tested using Jest.

## Step 3: Creating Your First Test File

Jest looks for test files with any of the following formats:

- Files with `.js` suffix in `__tests__` folders.
- Files with `.test.js` suffix.
- Files with `.spec.js` suffix.

To keep things simple, we'll create our test file in the same directory as our function. Create a file named `sum.test.js` and add the following code:

```javascript
const sum = require("./sum");

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

Here's what each part of the test file does:

- `const sum = require('./sum');` imports the function we want to test.
- `test('adds 1 + 2 to equal 3', () => {...});` defines a test case with a descriptive name and a function containing our test's logic.
- `expect(sum(1, 2)).toBe(3);` is an assertion that checks if calling `sum(1, 2)` returns `3`.

## Step 4: Running Your Test

With your test written, it's time to run it and see the results. Add the following script to your `package.json`:

```json
"scripts": {
  "test": "jest"
}
```

Now, run your test by executing:

```bash
npm test
```

Jest will execute the test and report the results. If everything is set up correctly, you should see output indicating that your test passed successfully.

## Congratulations!

You've just written and run your first test using Jest! This is just the beginning of your testing journey. As you become more comfortable with Jest, you'll discover its powerful features and how it can help you write better, more reliable code.

Remember, the key to effective testing is regular practice and experimentation. Happy testing!
