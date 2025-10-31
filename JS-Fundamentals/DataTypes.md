# Understanding Data Types in JavaScript

This document explains the fundamental data types in JavaScript. We will cover **Primitive Types** (the basic building blocks) and **Composite Types** (data structures), with a special focus on the most critical concept: **Pass by Value vs. Pass by Reference**.

## 🚀 Key Concepts Explained

Before we look at each type, let's define the two main categories of data in JavaScript. How the engine treats these categories is the most important concept to grasp.

### 1\. Primitive Types (Pass by Value)

A primitive is a simple, immutable (unchangeable) piece of data. When you assign a primitive value from one variable to another, the value is **copied**. They are compared **by their value**.

  * **Includes:** `String`, `Number`, `Boolean`, `Null`, `Undefined` (and `Symbol`, `BigInt`, which are more advanced).
  * **Storage:** The variable holds the *actual value* directly (this is a simplification, but it's the correct mental model).

### 2\. Composite Types (Pass by Reference)

A composite type (also called a "reference type") is a complex data structure that can hold multiple values. When you assign a composite type from one variable to another, you are **not copying the object**. You are only copying the **reference** (think of it as a memory address or a pointer) to that object.

  * **Includes:** `Object`, `Array` (which is a special type of object), and `Function`.
  * **Storage:** The variable holds a *reference* to a location in memory (the "heap") where the object is stored.

-----

## 🔵 Section 1: Primitive Types (Passed by Value)

These are the most basic data types. All primitives are **immutable**, meaning their value cannot be changed once created. You can only re-assign the variable to a *new* value.

### 1\. String

A `String` is used to store text. It is a sequence of characters wrapped in quotes.

```javascript
// 1. DECLARATION: Use single ('') or double ("") quotes.
let greeting = "Hello, world!";
let name = 'Alice';

console.log("1. String Value:", greeting);
console.log("1. String Type:", typeof greeting); // Outputs "string"
```

**Explanation:**

  * `greeting` and `name` are variables holding string-type data.
  * The `typeof` operator correctly identifies them as `"string"`.

### 2\. Number

A `Number` is used for all numeric values, including integers and floating-point (decimal) numbers.

```javascript
// 2. DECLARATION: Both integers and floats are 'number' type.
let age = 30;
let pi = 3.14159;

// Special numeric values
let notANumber = NaN; // "Not a Number"
let infinity = Infinity;

console.log("2. Number (Integer):", age);
console.log("2. Number (Float):", pi);
console.log("2. Number Type:", typeof age); // Outputs "number"
```

**Explanation:**

  * JavaScript does not have separate types for `int` or `float`; they are all just `number`.
  * `NaN` and `Infinity` are also special values of the `number` type.

### 3\. Boolean

A `Boolean` represents a logical entity and can have only two values: `true` or `false`.

```javascript
// 3. DECLARATION: No quotes are used.
let isLoggedIn = true;
let hasPermission = false;

console.log("3. Boolean Value:", isLoggedIn);
console.log("3. Boolean Type:", typeof isLoggedIn); // Outputs "boolean"
```

**Explanation:**

  * Booleans are the foundation of all logic and conditional statements (like `if` blocks).
  * `"true"` (a string) is completely different from `true` (a boolean).

### 4\. Undefined

A variable that has been declared but not assigned a value automatically has the value of `undefined`.

```javascript
// 4. DECLARATION: 'let' a variable without assigning a value.
let userStatus;

console.log("4. Undefined Value:", userStatus); // Outputs 'undefined'
console.log("4. Undefined Type:", typeof userStatus); // Outputs "undefined"
```

**Explanation:**

  * `undefined` represents the unintentional absence of a value. It's JavaScript's way of saying "I don't know what this is."

### 5\. Null

`Null` represents the **intentional** absence of any value. It must be explicitly assigned.

```javascript
// 5. DECLARATION: You must explicitly assign 'null'.
let selectedUser = null;

console.log("5. Null Value:", selectedUser); // Outputs 'null'

// This is a famous, long-standing bug in JavaScript!
console.log("5. Null Type (The 'Gotcha'):", typeof selectedUser); // Outputs "object"
```

**Explanation:**

  * You use `null` when you want to explicitly state that a variable has "no value."
  * **The `typeof null` Gotcha:** Due to a bug in the original implementation of JavaScript, `typeof null` returns `"object"`, not `"null"`. This is a quirk everyone must remember.

### 6\. Primitives Demonstration (Pass by Value)

This example shows how primitives are **copied**.

```javascript
// 6. PASS BY VALUE:
let a = 100;
let b = a; // The value 100 is COPIED from 'a' into 'b'.

console.log("6. Before:", { a, b }); // { a: 100, b: 100 }

// Now, let's change 'b'
b = 200;

console.log("6. After:", { a, b }); // { a: 100, b: 200 }
```

**Explanation:**

  * When we set `b = a`, `b` received a *copy* of the value `100`.
  * `a` and `b` are completely separate and independent.
  * Changing `b` has **no effect** on `a`.

-----

## 🟢 Section 2: Composite Types (Passed by Reference)

These types are collections of values or more complex entities. They are **mutable**, meaning their contents can be changed.

### 1\. Object

An `Object` is an **unordered** collection of key-value pairs. This is the most fundamental data structure in JavaScript.

```javascript
// 1. DECLARATION: Use curly braces {}.
const user = {
  firstName: "John",
  lastName: "Doe",
  age: 30
};

// Accessing properties
console.log("1. Object:", user);
console.log("1. Dot Notation:", user.firstName); // "John"
console.log("1. Bracket Notation:", user['age']); // 30

console.log("1. Object Type:", typeof user); // Outputs "object"
```

**Explanation:**

  * `firstName` is a **key** (or "property"), and `"John"` is its **value**.
  * You can access values using dot notation (e.g., `user.firstName`) or bracket notation (e.g., `user['firstName']`). Bracket notation is required when the key is a variable or contains special characters.

### 2\. Array

An `Array` is an **ordered** collection of values, accessed by a numeric index (starting at 0).

```javascript
// 2. DECLARATION: Use square brackets [].
const colors = ["red", "green", "blue", 10, true];

// Accessing elements
console.log("2. Array:", colors);
console.log("2. First Element (Index 0):", colors[0]); // "red"
console.log("2. Fourth Element (Index 3):", colors[3]); // 10
console.log("2. Array Length:", colors.length); // 5

// Arrays are just a special type of object
console.log("2. Array Type:", typeof colors); // Outputs "object"
```

**Explanation:**

  * Arrays are used for storing lists of data.
  * You access elements using their index (position) in brackets, starting from `[0]`.
  * Note that `typeof []` also returns `"object"`. You can check if it's an array using `Array.isArray(colors)`.

### 3\. Composite Demonstration (Pass by Reference "Gotcha")

This is the most critical "gotcha" for new developers. This behaves the exact same way as the `const` object.

```javascript
// 3. PASS BY REFERENCE:
const objA = { name: "Alex" };
const objB = objA; // We are NOT copying the object.
                  // We are copying the REFERENCE (the pointer) to the object.

console.log("3. Before:", objA.name); // "Alex"

// Now, let's change the name using 'objB'
objB.name = "Bob";

// We changed 'objB', but what happened to 'objA'?
console.log("3. After:", objA.name); // Outputs "Bob"
```

**Explanation:**

  * When we set `const objB = objA`, we did **not** create a new object.
  * Both `objA` and `objB` now point to the **exact same object** in memory.
  * When you modify the object using `objB` (e.g., `objB.name = "Bob"`), you are modifying the one and only object that `objA` *also* points to.
  * This is why changing `objB` appears to have changed `objA`. They are two names for the same thing.

-----

## 📊 Quick Summary Table

| Data Type | Example | `typeof` Output | Category | Mutable? |
| :--- | :--- | :--- | :--- | :--- |
| **String** | `"Hello"` | `"string"` | Primitive | No (Immutable) |
| **Number** | `123.45` | `"number"` | Primitive | No (Immutable) |
| **Boolean** | `true` | `"boolean"` | Primitive | No (Immutable) |
| **Undefined**| `undefined` | `"undefined"` | Primitive | No (Immutable) |
| **Null** | `null` | `"object"` | Primitive | No (Immutable) |
| **Object** | `{ a: 1 }` | `"object"` | Composite | **Yes (Mutable)** |
| **Array** | `[1, 2]` | `"object"` | Composite | **Yes (Mutable)** |
