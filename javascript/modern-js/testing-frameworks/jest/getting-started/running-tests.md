---
sidebar_position: 3
---

# Running Tests

Once you have written your tests using Jest, the next step is to run them to ensure your code behaves as expected. Jest offers a variety of options for running tests, from running all tests in your project to running specific tests or test suites. This guide will cover how to run your tests using Jest effectively.

## Basic Test Execution

To run all your tests with Jest, you can use the `npm test` script in your `package.json`. First, ensure you have the test script set up:

```json
"scripts": {
  "test": "jest"
}
```

Then, in your terminal, execute:

```bash
npm test
```

This command will run all tests in your project and output the results to the terminal.

## Running Tests in Watch Mode

During development, you might want to run tests related to files you've changed. Jest's watch mode makes this process efficient by automatically rerunning tests when it detects changes. To start Jest in watch mode, you can use the `--watch` flag:

```bash
npm test -- --watch
```

Or, if you're using Yarn:

```bash
yarn test --watch
```

## Running Specific Tests

If you want to run a specific test file or suite, you can pass the file name or pattern as an argument to Jest:

```bash
npm test -- sum.test.js
```

This command will only run tests found in the `sum.test.js` file.

## Using Test Patterns

To run tests that match a specific pattern, you can use the `--testNamePattern` or `-t` flag. This is useful for running all tests with a certain name or description:

```bash
npm test -- -t 'adds 1 + 2 to equal 3'
```

This command will run all tests with a description that includes 'adds 1 + 2 to equal 3'.

## Running Tests by Filename Pattern

You can also run tests from files that match a specific pattern using the `--findRelatedTests` flag. If you've made changes to a specific file and want to run all tests related to it, you can do so like this:

```bash
npm test -- --findRelatedTests path/to/yourFile.js
```

## Configuring Jest for Different Environments

Sometimes, you might need to run tests with different configurations or environments. You can specify a custom Jest configuration file using the `--config` flag:

```bash
npm test -- --config jest.config.dev.js
```

This allows you to maintain different configurations for development, CI environments, or specific testing scenarios.

## Viewing Test Coverage

Jest can generate a coverage report for your tests, helping you understand which parts of your codebase are not being tested. To enable this, use the `--coverage` flag:

```bash
npm test -- --coverage
```

This command will run your tests and produce a coverage report in the terminal. Jest also generates a more detailed HTML report in the `coverage/` directory.

## Conclusion

Running tests with Jest is straightforward, yet flexible enough to fit into any development workflow. Whether you're running all tests, focusing on specific tests during development, or generating coverage reports, Jest provides the tools you need to ensure your code is reliable and bug-free.

Remember, regular testing is key to maintaining a healthy codebase. Happy testing!
