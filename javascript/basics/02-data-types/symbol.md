---
sidebar_position: 7
---

# Symbol

Introduced in ECMAScript 2015 (ES6), the `Symbol` is a primitive data type unique to JavaScript. Unlike other primitive types, symbols are used as identifiers for object properties. Each symbol value is unique, making it an ideal candidate for naming object properties that need to be unique or for adding properties to objects without the risk of name conflicts.

## What is a Symbol?

- **Primitive Data Type**: Symbol is a primitive data type, just like `Number`, `String`, and `Boolean`.
- **Unique and Immutable**: Every symbol value returned by the `Symbol()` function is unique and immutable, meaning it cannot be changed once created.

## Creating Symbols

Symbols can be created using the `Symbol()` function. Optionally, you can provide a description (a string) that can be used for debugging but does not affect the uniqueness of the symbol.

```javascript
let mySymbol = Symbol("my unique symbol");
let anotherSymbol = Symbol("my unique symbol");

console.log(mySymbol === anotherSymbol); // Outputs: false
```

## Symbol Properties

### Description

The optional string description provided when creating a symbol can be accessed via the `description` property.

```javascript
let mySymbol = Symbol("description here");
console.log(mySymbol.description); // Outputs: "description here"
```

## Usage of Symbols

### Unique Object Keys

Symbols are often used to create unique keys for object properties to avoid property name collisions.

```javascript
const MY_KEY = Symbol();
let obj = {};

obj[MY_KEY] = 123;
console.log(obj[MY_KEY]); // Outputs: 123
```

### Symbol Registry

For symbols that need to be shared across different parts of code, the global symbol registry can be used. The methods `Symbol.for()` and `Symbol.keyFor()` allow setting and retrieving symbols from the registry.

```javascript
let globalSymbol = Symbol.for("globalSymbol");
let sameGlobalSymbol = Symbol.for("globalSymbol");

console.log(globalSymbol === sameGlobalSymbol); // Outputs: true
```

### Well-Known Symbols

JavaScript defines a set of well-known symbols that represent internal language behaviors that can be customized by developers. Examples include `Symbol.iterator`, `Symbol.asyncIterator`, and `Symbol.toStringTag`.

## Symbol Coercion

Symbols cannot be automatically converted to strings or numbers, preventing accidental type coercions that could lead to bugs. For example, attempting to concatenate a symbol with a string throws a TypeError.

```javascript
let mySymbol = Symbol("mySymbol");
console.log(String(mySymbol)); // Outputs: "Symbol(mySymbol)"
// console.log(mySymbol + ""); // This would throw a TypeError
```

## Conclusion

The `Symbol` type introduces a unique and powerful way to handle object property identifiers in JavaScript, ensuring property keys are unique and avoiding collisions. They also enable more complex object behaviors through well-known symbols. Understanding and utilizing symbols can enhance your JavaScript projects by providing more control over property iteration, privacy, and interactions with built-in JavaScript behaviors.

---
