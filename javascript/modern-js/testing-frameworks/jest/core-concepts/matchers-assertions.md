---
sidebar_position: 2
---

# Matchers and Assertions

In Jest, _matchers_ are methods that let you test values in various ways. An _assertion_, on the other hand, is a statement that checks if something is true. Essentially, every test you write will contain one or more assertions using matchers provided by Jest. Understanding these concepts is crucial for writing effective tests.

## Basic Matchers

Jest provides a rich set of matchers that you can use to test different things. Here are some of the most commonly used matchers:

### `toBe` and `toEqual`

- `toBe` uses `Object.is` to test exact equality. It's used for primitive values like strings, numbers, or booleans.

  ```javascript
  test("two plus two is four", () => {
    expect(2 + 2).toBe(4);
  });
  ```

- `toEqual` is used for more complex types like arrays or objects. It recursively checks every field of an object or array.

  ```javascript
  test("object assignment", () => {
    const data = { one: 1 };
    data["two"] = 2;
    expect(data).toEqual({ one: 1, two: 2 });
  });
  ```

### `toBeNull`, `toBeUndefined`, `toBeDefined`, `toBeTruthy`, `toBeFalsy`

These matchers let you test for specific conditions:

```javascript
test("null", () => {
  const n = null;
  expect(n).toBeNull();
  expect(n).toBeDefined();
  expect(n).not.toBeUndefined();
  expect(n).not.toBeTruthy();
  expect(n).toBeFalsy();
});
```

## Testing for Truthiness

In tests, you often need to check that a variable is true or false, or more generally, truthy or falsy. Jest provides matchers for these cases:

- `toBeNull` matches only `null`.
- `toBeUndefined` matches only `undefined`.
- `toBeDefined` is the opposite of `toBeUndefined`.
- `toBeTruthy` matches anything that an `if` statement treats as true.
- `toBeFalsy` matches anything that an `if` statement treats as false.

## Numbers

Jest offers a number of matchers for testing numbers:

```javascript
test("two plus two", () => {
  const value = 2 + 2;
  expect(value).toBeGreaterThan(3);
  expect(value).toBeGreaterThanOrEqual(3.5);
  expect(value).toBeLessThan(5);
  expect(value).toBeLessThanOrEqual(4.5);

  // toBe and toEqual are equivalent for numbers
  expect(value).toBe(4);
  expect(value).toEqual(4);
});
```

## Strings

You can check strings against regular expressions with `toMatch`:

```javascript
test("there is no I in team", () => {
  expect("team").not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
  expect("Christoph").toMatch(/stop/);
});
```

## Arrays and Iterables

To check if an array or iterable contains a particular item, you can use `toContain`:

```javascript
test("the shopping list has milk on it", () => {
  const shoppingList = [
    "diapers",
    "kleenex",
    "trash bags",
    "paper towels",
    "milk",
  ];
  expect(shoppingList).toContain("milk");
});
```

## Exceptions

If you want to test that a function throws an error when it's called, use `toThrow`:

```javascript
function compileAndroidCode() {
  throw new Error("you are using the wrong JDK");
}

test("compiling android goes as expected", () => {
  expect(compileAndroidCode).toThrow();
  expect(compileAndroidCode).toThrow(Error);

  // You can also use the exact error message or a regexp
  expect(compileAndroidCode).toThrow("you are using the wrong JDK");
  expect(compileAndroidCode).toThrow(/JDK/);
});
```

## Table of Matchers

This table is not exhaustive but covers a broad range of scenarios you'll likely encounter when writing tests.

| Matcher                            | Description                                                                                           |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `.toBe(value)`                     | Checks strict equality using `Object.is`.                                                             |
| `.toEqual(value)`                  | Checks for deep equality of objects or arrays.                                                        |
| `.toBeNull()`                      | Asserts that a value is `null`.                                                                       |
| `.toBeUndefined()`                 | Asserts that a value is `undefined`.                                                                  |
| `.toBeDefined()`                   | Asserts that a value is not `undefined`.                                                              |
| `.toBeTruthy()`                    | Asserts that a value is truthy (i.e., if it evaluates to true in a boolean context).                  |
| `.toBeFalsy()`                     | Asserts that a value is falsy (i.e., if it evaluates to false in a boolean context).                  |
| `.toBeGreaterThan(number)`         | Asserts that a number is greater than the given number.                                               |
| `.toBeGreaterThanOrEqual(number)`  | Asserts that a number is greater than or equal to the given number.                                   |
| `.toBeLessThan(number)`            | Asserts that a number is less than the given number.                                                  |
| `.toBeLessThanOrEqual(number)`     | Asserts that a number is less than or equal to the given number.                                      |
| `.toBeCloseTo(number, numDigits)`  | Asserts that a number is close to another number, accounting for floating point errors.               |
| `.toMatch(regexpOrString)`         | Asserts that a string matches a regular expression or string.                                         |
| `.toContain(item)`                 | Asserts that an array or iterable contains a specific item.                                           |
| `.toContainEqual(item)`            | Asserts that an array or iterable contains an element equal to the provided object or array.          |
| `.toHaveLength(number)`            | Asserts that an object has a `.length` property and it is set to a certain numeric value.             |
| `.toHaveProperty(keyPath, value?)` | Asserts that an object has a nested property. Optional value to check if the property is equal to it. |
| `.toThrow(error?)`                 | Asserts that a function throws an error when it is called. Optional argument to specify the error.    |
| `.not`                             | Inverts the matcher that follows it.                                                                  |

## Conclusion

Matchers and assertions are powerful tools in Jest that allow you to write expressive and concise tests. By understanding and utilizing the wide range of matchers available, you can effectively test your code under various conditions and ensure your applications work as intended.
