---
sidebar_position: 1
---

# Installation & Set Up

Installing and setting up Jest in a JavaScript or TypeScript project involves a few straightforward steps. This guide will cover the basics to get you started with Jest for both simple JavaScript projects and projects using modern tools like Babel or TypeScript.

### Prerequisites

Before installing Jest, ensure you have Node.js installed in your development environment. Jest requires Node.js to run, and having npm (Node Package Manager) makes the installation process simpler. You can check if Node.js and npm are installed by running the following commands in your terminal:

```bash
node --version
npm --version
```

### Installation

#### For a Basic JavaScript Project

1. **Initialize your project (if you haven't already):**

   If you're starting a new project, first initialize it with npm. In your project directory, run:

   ```bash
   npm init -y
   ```

   This command creates a `package.json` file in your project directory.

2. **Install Jest:**

   To install Jest as a development dependency, run:

   ```bash
   npm install --save-dev jest
   ```

   This command adds Jest to the `devDependencies` in your `package.json` file.

#### For Projects Using Babel

If your project uses ES6 or later features that Node.js doesn't support natively, you'll likely use Babel to transpile your code. To use Jest with Babel, you need to install some additional dependencies:

1. **Install Babel and Jest:**

   ```bash
   npm install --save-dev jest @babel/core @babel/preset-env
   ```

2. **Configure Babel:**

   Create a `.babelrc` file in your project root or add a `babel` section in your `package.json` file with the following content to tell Babel how to transpile your code:

   ```json
   {
     "presets": ["@babel/preset-env"]
   }
   ```

#### For TypeScript Projects

Jest can directly work with TypeScript using the `ts-jest` package.

1. **Install Jest and ts-jest:**

   ```bash
   npm install --save-dev jest ts-jest @types/jest typescript
   ```

2. **Configure Jest for TypeScript:**

   Create a `jest.config.js` file in your project root with the following configuration:

   ```javascript
   module.exports = {
     preset: "ts-jest",
     testEnvironment: "node",
   };
   ```

### Configuration

Jest works out of the box with minimal configuration for most JavaScript projects. However, customizing the Jest configuration allows you to tailor the testing environment to your project's needs. Configuration can be done in the `package.json` file under the `"jest"` key, or by creating a standalone `jest.config.js` file in your project root. Here's an example `jest.config.js`:

```javascript
module.exports = {
  verbose: true,
  testEnvironment: "node",
  // Add more configuration options as needed
};
```

### Writing Your First Test

Create a file named `sum.test.js` (or `sum.test.ts` for TypeScript) with the following content:

```javascript
function sum(a, b) {
  return a + b;
}

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

### Running Tests

To run your tests, add the following script to your `package.json`:

```json
"scripts": {
  "test": "jest"
}
```

Now, you can run your tests by executing:

```bash
npm test
```

### Watching Tests

For a more interactive testing experience, Jest can watch your files for changes and rerun tests related to changed files. Start Jest in watch mode with:

```bash
npm test -- --watch
```

This setup covers the basics of installing and configuring Jest in your JavaScript or TypeScript project. As you become more familiar with Jest, you can explore its comprehensive configuration options and advanced features to better suit your testing requirements.
