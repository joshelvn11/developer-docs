---
sidebar_position: 4
---

# Numbers

JavaScript provides a single number type for both integer and floating-point values, simplifying the handling of numeric values in the language. Unlike some other languages that distinguish between types for integer and floating-point numbers, JavaScript uses the IEEE 754 standard for its number representation, which allows for a wide range of numeric values, including special ones like `Infinity` and `NaN` ("Not a Number"). Here's a closer look at numbers in JavaScript.

## Number Type

- **IEEE 754 Standard**: JavaScript's number system is based on the IEEE 754 standard, using double-precision 64-bit binary format. This encompasses both integers and floating-point numbers within the same `number` type.

- **Range**: This format allows for numbers between 5e-324 (minimum positive subnormal) and 1.7976931348623157e+308 (maximum positive number).

## Creating Number Values

Numbers can be assigned to variables directly. JavaScript interprets numeric literals as numbers:

```javascript
let integerExample = 42;
let floatingPointExample = 3.14;
```

## Special Numeric Values

JavaScript numbers include a few special values:

### `Infinity`

- Represents mathematical infinity. It is a value greater than any other number.
- Division by zero (except 0/0) results in `Infinity`.

```javascript
console.log(1 / 0); // Outputs: Infinity
```

### `-Infinity`

- Represents negative infinity, less than any other number.

```javascript
console.log(-1 / 0); // Outputs: -Infinity
```

### `NaN`

- Stands for "Not a Number", used to denote an undefined or unrepresentable result.
- Operations resulting in `NaN` include dividing 0/0 or taking the square root of a negative number.

```javascript
console.log(0 / 0); // Outputs: NaN
```

## Precision and Limitations

- **Safe Integer Limit**: The largest safe integer in JavaScript is `2^53 - 1` (`9007199254740991`), and the smallest is `-(2^53 - 1)`. These are defined as `Number.MAX_SAFE_INTEGER` and `Number.MIN_SAFE_INTEGER`.
- **Floating-Point Arithmetic**: Due to the binary nature of their encoding, some floating-point numbers cannot be represented with perfect accuracy.

```javascript
console.log(0.1 + 0.2); // Outputs: 0.30000000000000004
```

## Useful Number Methods

JavaScript's `Number` object includes several methods and properties for numeric operations:

- `Number.isFinite(value)`: Checks if the value is a finite number.
- `Number.isInteger(value)`: Checks if the value is an integer.
- `Number.isNaN(value)`: Checks if the value is `NaN`.
- `Number.parseFloat(string)`: Parses the argument as a floating point number.
- `Number.parseInt(string, radix)`: Parses the argument as an integer.

## Numeric Conversions

Implicit conversions happen often in JavaScript. For instance, when performing operations that expect a number on a non-numeric value:

```javascript
console.log("6" / "2"); // Outputs: 3
```

Explicit conversions can be performed using the `Number()` function, unary plus `+`, or other methods like `parseInt()` and `parseFloat()`.

## Methods

JavaScript provides a set of methods on the `Number` object that are useful for various numerical operations. These methods allow for parsing, checking, and transforming number values. Below is a full list of these methods along with a brief description of each.

| Method                                             | Description                                                                                                                                                                                                                                           |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Number.isFinite(value)`                           | Determines whether the passed value is a finite number. Unlike the global `isFinite`, `Number.isFinite` doesn't forcibly convert the parameter to a number. This means only finite values of the type number, not `NaN` or `Infinity`, return `true`. |
| `Number.isInteger(value)`                          | Determines whether the provided value is an integer.                                                                                                                                                                                                  |
| `Number.isNaN(value)`                              | Determines whether the provided value is `NaN`. This is more robust than the original global `isNaN()`, which coerces the value to a number and might lead to false positives.                                                                        |
| `Number.isSafeInteger(value)`                      | Determines whether the provided value is a number that is a safe integer. A safe integer is an integer that can be exactly represented as an IEEE-754 double precision number (between -(2^53 - 1) and 2^53 - 1).                                     |
| `Number.parseFloat(string)`                        | Parses a string argument and returns a floating point number. Equivalent to the global `parseFloat()` function.                                                                                                                                       |
| `Number.parseInt(string, radix)`                   | Parses a string argument and returns an integer of the specified radix or base. Equivalent to the global `parseInt()` function.                                                                                                                       |
| `Number.prototype.toFixed(digits)`                 | Formats a number using fixed-point notation, returning a string.                                                                                                                                                                                      |
| `Number.prototype.toExponential(fractionDigits)`   | Returns a string representing the number in exponential notation.                                                                                                                                                                                     |
| `Number.prototype.toPrecision(precision)`          | Returns a string representing the number to a specified precision in fixed or exponential notation.                                                                                                                                                   |
| `Number.prototype.toString(radix)`                 | Returns a string representing the specified object in the specified radix (base).                                                                                                                                                                     |
| `Number.prototype.toLocaleString(locale, options)` | Returns a string with a language-sensitive representation of this number. It overrides the `Object.prototype.toLocaleString()` method.                                                                                                                |
| `Number.prototype.valueOf()`                       | Returns the primitive value of the specified object.                                                                                                                                                                                                  |

## Static Properties

In addition to methods, `Number` also has static properties that provide maximum and minimum values, among others:

| Property                   | Description                                                                                |
| -------------------------- | ------------------------------------------------------------------------------------------ |
| `Number.MAX_SAFE_INTEGER`  | Represents the maximum safe integer in JavaScript (`9007199254740991`).                    |
| `Number.MIN_SAFE_INTEGER`  | Represents the minimum safe integer in JavaScript (`-9007199254740991`).                   |
| `Number.MAX_VALUE`         | Represents the largest positive representable number.                                      |
| `Number.MIN_VALUE`         | Represents the smallest positive representable number (closest to zero).                   |
| `Number.NaN`               | Represents "Not-a-Number" value.                                                           |
| `Number.EPSILON`           | Represents the difference between 1 and the smallest floating point number greater than 1. |
| `Number.POSITIVE_INFINITY` | Represents the positive Infinity value.                                                    |
| `Number.NEGATIVE_INFINITY` | Represents the negative Infinity value.                                                    |

Understanding and utilizing these methods and properties can significantly aid in number manipulation and evaluation in JavaScript programming.

---

## Conclusion

Numbers in JavaScript are versatile, supporting a wide range of numerical operations with a single number type. Understanding the characteristics, limitations, and special values of JavaScript numbers is crucial for effective programming, especially in applications involving mathematical calculations, data processing, and any scenario where precision is key.
