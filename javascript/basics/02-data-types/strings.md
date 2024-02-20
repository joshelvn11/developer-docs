---
sidebar_position: 6
---

# Strings

Strings in JavaScript are used to represent and manipulate textual data. They are one of the primitive data types in JavaScript, meaning they are immutable and cannot be changed once they are created. This characteristic has implications for how strings are handled in operations and functions. Here's a closer look at strings in JavaScript.

## Definition

A string can be defined as a sequence of characters used to represent text. In JavaScript, strings can be created using either single quotes (`'`), double quotes (`"`), or template literals (`` ` ``).

### Examples

```javascript
let singleQuoted = "Hello, world!";
let doubleQuoted = "Hello, world!";
let templateLiteral = `Hello, world!`;
```

## Characteristics

### Immutability

Strings are immutable, which means once a string is created, it cannot be altered. Any operation that appears to change a string actually creates a new string.

```javascript
let greeting = "Hello";
greeting[0] = "J"; // Trying to change 'H' to 'J'
console.log(greeting); // Outputs: Hello
```

### Unicode

JavaScript strings are UTF-16 encoded, meaning they can easily represent any unicode character.

```javascript
let smile = "😊";
console.log(smile); // Outputs: 😊
```

## Common Operations

### Concatenation

Strings can be concatenated using the `+` operator or template literals for more complex constructions.

```javascript
let hello = "Hello,";
let world = "world!";
let greeting = hello + " " + world; // Using +
console.log(greeting); // Outputs: Hello, world!

let greetingTemplate = `${hello} ${world}`; // Using template literal
console.log(greetingTemplate); // Outputs: Hello, world!
```

### Length

The `length` property provides the number of characters in a string.

```javascript
let text = "Hello, world!";
console.log(text.length); // Outputs: 13
```

### Accessing Characters

Individual characters in a string can be accessed using bracket notation or the `charAt()` method.

```javascript
let text = "Hello, world!";
console.log(text[0]); // Outputs: H
console.log(text.charAt(1)); // Outputs: e
```

### Searching and Replacing

JavaScript provides methods like `indexOf()`, `lastIndexOf()`, `startsWith()`, `endsWith()`, and `replace()` for searching and replacing within strings.

```javascript
let text = "Hello, world!";
console.log(text.indexOf("world")); // Outputs: 7
console.log(text.replace("world", "everyone")); // Outputs: Hello, everyone!
```

### Case Conversion

The methods `toUpperCase()` and `toLowerCase()` are used to convert strings to upper or lower case, respectively.

```javascript
let text = "Hello, World!";
console.log(text.toUpperCase()); // Outputs: HELLO, WORLD!
console.log(text.toLowerCase()); // Outputs: hello, world!
```

### Splitting and Joining

The `split()` method divides a string into an ordered list of substrings, puts these substrings into an array, and returns the array. The `join()` method is used to join all elements of an array into a string.

```javascript
let text = "Hello, world!";
let words = text.split(", "); // Splits the string into an array
console.log(words); // Outputs: ["Hello", "world!"]

let joinedText = words.join(", "); // Joins the array back into a string
console.log(joinedText); // Outputs: Hello, world!
```

### Template Literals

Template literals provide an easy way to create multiline strings and to perform string interpolation. They are enclosed by the backtick (`` ` ``) character.

```javascript
let name = "John";
let greeting = `Hello, ${name}!
How are you today?`;
console.log(greeting);
```

## String Methods

| Method                                | Description                                                                                                                    |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `charAt(index)`                       | Returns the character at the specified index.                                                                                  |
| `charCodeAt(index)`                   | Returns the Unicode of the character at the specified index.                                                                   |
| `concat(...strings)`                  | Concatenates the string arguments to the calling string.                                                                       |
| `includes(searchString, position)`    | Determines whether one string may be found within another string.                                                              |
| `endsWith(searchString, length)`      | Determines whether a string ends with the characters of a specified string.                                                    |
| `indexOf(searchValue, fromIndex)`     | Returns the index of the first occurrence of a specified value.                                                                |
| `lastIndexOf(searchValue, fromIndex)` | Returns the index of the last occurrence of a specified value.                                                                 |
| `localeCompare(compareString)`        | Returns a number indicating whether a reference string comes before or after or is the same as the given string in sort order. |
| `match(regexp)`                       | Matches a string against a regular expression pattern.                                                                         |
| `matchAll(regexp)`                    | Returns an iterator of all results matching a string against a regular expression, including capturing groups.                 |
| `normalize(form)`                     | Returns the Unicode Normalization Form of the calling string value.                                                            |
| `padEnd(targetLength, padString)`     | Pads the current string from the end with a given string to create a new string of a certain length.                           |
| `padStart(targetLength, padString)`   | Pads the current string from the start with a given string to create a new string of a certain length.                         |
| `repeat(count)`                       | Returns a new string consisting of the elements of the object repeated the given times.                                        |
| `replace(searchFor, replaceWith)`     | Replaces matches for `searchFor` in the string with `replaceWith`. Can accept a string or a RegExp for `searchFor`.            |
| `replaceAll(searchFor, replaceWith)`  | Replaces all matches for `searchFor` in the string with `replaceWith`. Can accept a string or a RegExp for `searchFor`.        |
| `search(regexp)`                      | Searches the string for a match to the regular expression given in argument.                                                   |
| `slice(beginIndex, endIndex)`         | Extracts a section of a string and returns it as a new string, without modifying the original string.                          |
| `split(separator, limit)`             | Splits a String object into an array of strings by separating the string into substrings.                                      |
| `startsWith(searchString, position)`  | Determines whether a string begins with the characters of a specified string.                                                  |
| `substring(indexStart, indexEnd)`     | Returns a new string containing characters of the calling string from (or between) the specified index (or indices).           |
| `toLocaleLowerCase()`                 | Returns the calling string value converted to lower case, according to any locale-specific case mappings.                      |
| `toLocaleUpperCase()`                 | Returns the calling string value converted to upper case, according to any locale-specific case mappings.                      |
| `toLowerCase()`                       | Returns the calling string value converted to lowercase.                                                                       |
| `toString()`                          | Returns a string representing the specified object. Overrides the `Object.prototype.toString()` method.                        |
| `toUpperCase()`                       | Returns the calling string value converted to uppercase.                                                                       |
| `trim()`                              | Trims whitespace from the beginning and end of the string.                                                                     |
| `trimEnd()` or `trimRight()`          | Trims whitespace from the end of a string.                                                                                     |
| `trimStart()` or `trimLeft()`         | Trims whitespace from the beginning of a string.                                                                               |
| `valueOf()`                           | Returns the primitive value of the specified object. Overrides the `Object.prototype.valueOf()` method.                        |

## Conclusion

Strings in JavaScript are powerful and flexible, allowing for a wide range of manipulations and operations to handle textual data efficiently. Understanding how to work with strings is fundamental to JavaScript programming, especially when dealing with user input, data manipulation, and output.
