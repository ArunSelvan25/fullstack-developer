# Understanding Conditionals in JavaScript

This document explains how to use conditional statements in JavaScript to make decisions and run different blocks of code. We will cover `if`, `else`, `else if`, the **Ternary Operator**, and `switch`, as well as the **Comparison** and **Logical Operators** used to build them.

## 🚀 Key Concepts Explained

Before we build full statements, we must understand the "questions" we can ask. These are formed using comparison and logical operators.

### 1\. Comparison Operators

Comparison operators compare two values and return a `Boolean` (`true` or `false`).

| Operator | Name | Example | Result |
| :--- | :--- | :--- | :--- |
| `>` | Greater Than | `10 > 5` | `true` |
| `<` | Less Than | `10 < 5` | `false` |
| `>=` | Greater Than or Equal | `5 >= 5` | `true` |
| `<=` | Less Than or Equal | `4 <= 5` | `true` |
| `!=` | Loose Not-Equal | `10 != '10'` | `false` |
| `!==` | Strict Not-Equal | `10 !== '10'`| `true` |
| `==` | Loose Equals | `10 == '10'` | `true` |
| `===` | Strict Equals | `10 === '10'`| `false` |

### 2\. The "Gotcha": Strict (`===`) vs. Loose (`==`) Equality

This is one of the most common sources of bugs in JavaScript.

  * **`===` (Strict Equals):** Checks for both **value** AND **type**. This is what you should use 99% of the time.
  * **`==` (Loose Equals):** Tries to **"coerce"** (convert) the types to match *before* comparing the value.

```javascript
// 2. STRICT vs. LOOSE "Gotcha"
let num = 10;
let str = "10";

// Loose (==) converts the string "10" to a number 10, then compares.
console.log("2. Loose (==):", num == str); // Outputs: true (BUGGY!)

// Strict (===) checks the type. A 'number' is not a 'string'.
console.log("2. Strict (===):", num === str); // Outputs: false (SAFE)
```

**Explanation:**
The loose comparison `num == str` sees a number and a string, so it converts the string `"10"` to the number `10` and then asks, "Does `10` equal `10`?" This is `true`.
The strict comparison `num === str` sees a `number` and a `string` and immediately returns `false` because the types are different. No conversion is attempted.

**Rule of Thumb: Always use `===` and `!==` unless you have a specific reason to use `==`.**

### 3\. Logical Operators

Logical operators are used to **combine** multiple `true`/`false` conditions into one.

```javascript
let age = 25;
let hasLicense = true;

// 3a. && (AND): BOTH sides must be true.
// "Is age over 18 AND do they have a license?"
let canDrive = (age > 18) && (hasLicense === true);
console.log("3a. AND (&&):", canDrive); // Outputs: true

// 3b. || (OR): AT LEAST ONE side must be true.
let isStudent = false;
let isSenior = true;
// "Are they a student OR are they a senior?"
let getsDiscount = isStudent || isSenior;
console.log("3b. OR (||):", getsDiscount); // Outputs: true

// 3c. ! (NOT): Reverses the boolean value.
let isWorking = true;
let isFree = !isWorking;
console.log("3c. NOT (!):", isFree); // Outputs: false
```

### 4\. The "Gotcha": Truthy and Falsy Values

JavaScript has a concept of "truthy" and "falsy." When JavaScript expects a `boolean` (like in an `if` statement), it will "coerce" any value into one.

  * **Falsy:** All values that convert to `false`. There are only 6:
    1.  `false`
    2.  `0` (the number zero)
    3.  `""` (an empty string)
    4.  `null`
    5.  `undefined`
    6.  `NaN` (Not a Number)
  * **Truthy:** **Everything else.** Any string with content (`"Hello"`, `"0"`), any number (except `0`), all objects (`{}`), and all arrays (`[]`) are `true`.

```javascript
// 4. TRUTHY / FALSY "Gotcha"
let userName = ""; // This is a FALSY value

if (userName) {
  // This block will NOT run because "" is falsy.
  console.log("4. User name exists!");
} else {
  // This block WILL run.
  console.log("4. Falsy: Please provide a user name.");
}

let items = []; // An empty array is TRUTHY!
if (items) {
  // This block WILL run.
  console.log("4. Truthy: The items array exists.");
}
```

-----

## 🔵 Section 1: The `if` Statement

The `if` statement is the most basic conditional. It runs a block of code *only if* its condition is `true`.

```javascript
// 1. 'if' Statement
let temperature = 30;

console.log("1. Checking temperature...");

if (temperature > 25) {
  // This code block runs because 30 > 25 is true.
  console.log("1. It's a hot day!");
}

console.log("1. Check complete.");
```

**Explanation:**

  * The code first checks the condition `(temperature > 25)`.
  * This evaluates to `true`, so the code inside the curly braces `{ ... }` is executed.
  * If the temperature were `20`, the condition would be `false`, and the block would be skipped.

-----

## 🟢 Section 2: The `else` Statement

The `else` statement provides a **fallback** block of code to run if the `if` condition was `false`.

```javascript
// 2. 'if...else' Statement
let age = 16;

if (age >= 18) {
  // This block is SKIPPED because 16 >= 18 is false.
  console.log("2. You are old enough to vote.");
} else {
  // This block is EXECUTED because the 'if' condition was false.
  console.log("2. You are not old enough to vote.");
}
```

**Explanation:**

  * The `if` condition `(age >= 18)` is `false`.
  * Because the `if` failed, the code "falls back" to the `else` block and executes the code inside it.
  * An `else` block can *only* exist after an `if` block.

-----

## 🟡 Section 3: The `else if` Statement

The `else if` statement lets you **chain multiple conditions**. It checks them one by one, in order, and stops as soon as one is `true`.

```javascript
// 3. 'if...else if...else' Statement
let score = 85;

if (score >= 90) {
  // 1st check: Is 85 >= 90? (False) -> Skipped.
  console.log("3. Grade: A");
} else if (score >= 80) {
  // 2nd check: Is 85 >= 80? (True) -> EXECUTED.
  console.log("3. Grade: B");
} else if (score >= 70) {
  // 3rd check: SKIPPED. (The chain stops after one 'true' result).
  console.log("3. Grade: C");
} else {
  // Fallback: SKIPPED.
  console.log("3. Grade: F");
}
```

**Explanation:**

  * JavaScript checks the conditions **in order from top to bottom**.
  * `score >= 90` is `false`.
  * It moves to the next check: `score >= 80`. This is `true`.
  * It executes the `console.log("3. Grade: B")` block.
  * **Crucially**, it **stops checking** and skips all remaining `else if` and `else` blocks in the chain.

-----

## 🟣 Section 4: The Ternary Operator

The **ternary operator** (also called the Conditional Operator) is a compact, one-line shortcut for a standard `if...else` statement. Its main purpose is to return one of two values based on a condition.

**Syntax:** `condition ? valueIfTrue : valueIfFalse`

### 1\. Basic Ternary vs. `if...else`

It's easiest to understand by seeing it next to the `if...else` it replaces.

```javascript
let age = 16;

// METHOD 1: Using 'if...else' (Multiple lines)
let message;
if (age >= 18) {
  message = "You can vote.";
} else {
  message = "You cannot vote.";
}
console.log("1. 'if...else' message:", message);

// METHOD 2: Using Ternary Operator (One line)
let ternaryMessage = (age >= 18) ? "You can vote." : "You cannot vote.";
console.log("1. Ternary message:", ternaryMessage);
```

**Explanation:**

  * `(age >= 18)` is the **condition** being checked.
  * The `?` (question mark) separates the condition from the results.
  * `"You can vote."` is the value assigned to `ternaryMessage` if the condition is **true**.
  * The `:` (colon) separates the true value from the false value.
  * `"You cannot vote."` is the value assigned to `ternaryMessage` if the condition is **false**.

### 2\. "Gotcha": Readability (Don't Overuse It)

While ternaries are great for simple assignments, they can become very difficult to read if they are "nested" (a ternary inside another ternary).

```javascript
// 2. "GOTCHA": A nested ternary
let score = 85;

// This works, but it's hard to read and debug.
let grade = (score >= 90) ? "A" :
            (score >= 80) ? "B" :
            (score >= 70) ? "C" : "F";

console.log("2. Nested ternary grade:", grade); // Outputs "B"
```

**Explanation:**

  * This is a common "clever" trick, but it's usually bad practice.
  * The code asks, "Is score \>= 90? If yes, 'A'. If no (`:`), ask another question: Is score \>= 80? If yes, 'B'. If no (`:`)..."
  * In this situation, a standard `if...else if` chain (as shown in Section 3) is **much clearer and easier to maintain**. Use ternaries only for simple `true`/`false` choices.

-----

## 🔴 Section 5: The `switch` Statement

A `switch` statement is a cleaner alternative to a long `if...else if` chain *when you are comparing one single variable against many possible values*.

### 1\. `switch` with `break`

The `break` keyword is essential. It tells JavaScript to "break out" of the `switch` block after a `case` is matched.

```javascript
// 1. Basic 'switch' Statement
let userRole = "admin";

switch (userRole) {
  case "admin":
    console.log("1. You have full access.");
    break; // Stops here.

  case "editor":
    console.log("1. You can write and edit content.");
    break;

  case "guest":
    console.log("1. You have read-only access.");
    break;

  default:
    // 'default' is like 'else'. It runs if no other case matches.
    console.log("1. Unknown role.");
}
```

**Explanation:**

  * `switch (userRole)` tells JavaScript to check the value of `userRole`.
  * It looks for a `case` that matches `"admin"`. It finds `case "admin":`.
  * It runs the code `console.log("1. You have full access.")`.
  * It hits the `break;` keyword and immediately exits the `switch` block.

### 2\. `switch` "Gotcha": Missing `break` (Fall-through)

If you forget `break`, the code will "fall through" and execute the code in the *next* `case` as well, which is almost always a bug.

```javascript
// 2. "Gotcha" - Missing 'break'
let day = "Monday";

switch (day) {
  case "Monday":
    console.log("2. Starting the work week.");
    // NO 'break' - this is a bug!

  case "Tuesday":
    console.log("2. Back to work."); // This runs too!
    break;

  case "Friday":
    console.log("2. Ready for the weekend!");
    break;
}
```

**Explanation:**

  * The `switch` matches `case "Monday":` and runs the `console.log`.
  * Because there is no `break;`, execution "falls through" directly to `case "Tuesday":` and runs its code *without checking if `day` is "Tuesday"*.
  * It finally hits a `break;` and exits. The output would be:
      * `"2. Starting the work week."`
      * `"2. Back to work."`

-----

## 📊 Quick Summary Tables

### Comparison Operators

| Operator | Name | Use `===` (Strict) | Use `==` (Loose) |
| :--- | :--- | :--- | :--- |
| `===` | Strict Equals | **Yes** (Best Practice) | |
| `==` | Loose Equals | | No (Avoid) |
| `!==` | Strict Not-Equals | **Yes** (Best Practice) | |
| `!=` | Loose Not-Equals | | No (Avoid) |
| `>` | Greater Than | (N/A) | (N/A) |
| `<` | Less Than | (N/A) | (N/A) |
| `>=` | Greater/Equal | (N/A) | (N/A) |
| `<=` | Less/Equal | (N/A) | (N/A) |

### Logical Operators

| Operator | Name | What it means |
| :--- | :--- | :--- |
| `&&` | AND | **Both** sides must be true. |
| `\|\|` | OR | **At least one** side must be true. |
| `!` | NOT | Reverses the value (`true` -\> `false`) |
