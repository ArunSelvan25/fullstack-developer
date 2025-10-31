# Understanding Loops in JavaScript

This document explains how to use loops in JavaScript to run a block of code repeatedly. We will cover `for`, `while`, `do...while`, and `for...of`, as well as the **Loop Control** keywords `break` and `continue`.

## 🚀 Key Concepts Explained

Before we look at each loop type, let's define the key concepts.

### 1\. Iteration

An **iteration** is a single pass or execution of the code block inside a loop. If a loop runs 5 times, it has performed 5 iterations.

### 2\. The Counter (e.g., `i`)

In many loops, you need a variable to track "which iteration am I on?" This variable is called a **counter** or **iterator**. By convention, it's almost always named `i` (for "index"). In the next loop, if you need another counter, it's `j`, then `k`, and so on.

### 3\. The "Gotcha": Infinite Loops

A loop will run forever if its exit condition is **never** met. This is a common bug called an **infinite loop**, and it will freeze your program or browser tab.

```javascript
// 3. INFINITE LOOP "Gotcha" - DO NOT RUN THIS!
let i = 0;
while (i < 10) {
  // This code will run forever.
  console.log("I am looping!");
  // BUG: We forgot to add 'i++' to change the condition.
  // 'i' will always be 0, and 0 is always less than 10.
}
```

**Explanation:** The condition `i < 10` is checked, `i` is `0`, so the loop runs. Then the condition is checked again... `i` is *still* `0`. The condition will never become `false`, so the loop never stops.

-----

## 🔵 Section 1: The `for` Loop

The `for` loop is the most common and versatile loop. You use it when you **know how many times** you want the loop to run (e.g., "run 10 times," "loop through all 50 items in this list").

It has three parts separated by semicolons: `for (initialization; condition; increment)`

1.  **Initialization:** Runs *once* before the loop starts. Used to create your counter (e.g., `let i = 0`).
2.  **Condition:** Checked *before* every iteration. If `true`, the loop runs. If `false`, the loop stops.
3.  **Increment:** Runs *after* every iteration. Used to update your counter (e.g., `i++`).

### 1\. `for` Loop Example (Counting)

```javascript
// 1. A 'for' loop that runs 5 times.
console.log("1. 'for' loop starting...");

// 1. Initialization: let i = 0 (Start 'i' at 0)
// 2. Condition: i < 5 (Run as long as 'i' is less than 5)
// 3. Increment: i++ (Add 1 to 'i' after each loop)
for (let i = 0; i < 5; i++) {
  // This block runs for i = 0, 1, 2, 3, 4
  console.log("1. The current number is:", i);
}

console.log("1. 'for' loop finished.");
```

**Execution Flow:**

  * **Start:** `let i = 0` is run. `i` is now `0`.
  * **Iteration 1:** Check condition `(0 < 5)`. It's `true`.
      * Run block: `console.log` prints `0`.
      * Increment: `i++` runs. `i` is now `1`.
  * **Iteration 2:** Check condition `(1 < 5)`. It's `true`.
      * Run block: `console.log` prints `1`.
      * Increment: `i++` runs. `i` is now `2`.
  * ... (Iterations 3 and 4 for `i = 2` and `i = 3`) ...
  * **Iteration 5:** Check condition `(4 < 5)`. It's `true`.
      * Run block: `console.log` prints `4`.
      * Increment: `i++` runs. `i` is now `5`.
  * **Final Check:** Check condition `(5 < 5)`. It's `false`.
  * **Stop:** The loop terminates.

-----

## 🟢 Section 2: The `while` Loop

The `while` loop is simpler. You use it when you **don't know how many iterations** you need, but you know the *condition* that must be met to keep going (e.g., "keep asking for a password until it's correct," "keep dealing cards while the player has less than 21").

**Syntax:** `while (condition) { ... }`

The condition is checked **before** the block runs.

### 1\. `while` Loop Example

```javascript
// 1. A 'while' loop for a countdown.
console.log("1. 'while' loop starting...");
let count = 3;

while (count > 0) {
  // Condition is checked. (3 > 0) is true.
  console.log("1. T-minus " + count);

  // We MUST update the variable inside the loop!
  count--; // count = count - 1
}

console.log("1. Liftoff!");
```

**Explanation:**

  * **Check 1:** `count > 0` (3 \> 0) is `true`. Run block. Prints "T-minus 3". `count` becomes 2.
  * **Check 2:** `count > 0` (2 \> 0) is `true`. Run block. Prints "T-minus 2". `count` becomes 1.
  * **Check 3:** `count > 0` (1 \> 0) is `true`. Run block. Prints "T-minus 1". `count` becomes 0.
  * **Check 4:** `count > 0` (0 \> 0) is `false`.
  * **Stop:** The loop terminates.

### 2\. "Gotcha": Loop May Never Run

If the condition is `false` to begin with, a `while` loop will **never run**.

```javascript
// 2. "Gotcha" - Loop never runs
let age = 20;
while (age < 18) {
  // This code is NEVER executed, because (20 < 18) is false.
  console.log("2. You are not old enough.");
}
```

-----

## 🟡 Section 3: The `do...while` Loop

This loop is a variant of `while`. Its key feature is that the condition is checked **after** the loop body runs.

This **guarantees the code block will run at least once**, even if the condition is `false`.

**Syntax:** `do { ... } while (condition);`

### 1\. `do...while` Loop Example

This is perfect for a menu that must be shown at least once.

```javascript
// 1. 'do...while' example
console.log("1. 'do...while' loop starting...");
let choice;

do {
  // This block is GUARANTEED to run at least once.
  console.log("1. Please select an option:");
  console.log("   Enter 'q' to quit.");
  
  // In a real app, you'd get user input. We'll fake it.
  choice = 'q'; // We assign 'q' so the loop stops.

} while (choice !== 'q'); // Condition is checked AFTER the block.

console.log("1. Quitting program.");
```

**Explanation:**

  * The `do { ... }` block runs immediately, printing the menu.
  * `choice` is set to `'q'`.
  * The `while (choice !== 'q')` condition is checked. `('q' !== 'q')` is `false`.
  * **Stop:** The loop terminates. If we had set `choice = 'a'`, the loop would have run again.

-----

## 🔴 Section 4: The `for...of` Loop (Modern Iteration)

The `for...of` loop (introduced in ES6) is the simplest and cleanest way to loop over every item in an **iterable** (like an `Array`).

It completely handles the counter (`i`) and condition (`< array.length`) for you.

**Syntax:** `for (const item of array) { ... }`

### 1\. `for...of` vs. `for` Loop Example

```javascript
const colors = ["red", "green", "blue"];

// METHOD 1: The "old" way with a 'for' loop
console.log("1. 'for' loop (old way):");
for (let i = 0; i < colors.length; i++) {
  // We have to use 'i' to get the value
  console.log("1.", colors[i]);
}

// METHOD 2: The "modern" way with a 'for...of' loop
console.log("2. 'for...of' loop (modern way):");
for (const color of colors) {
  // 'color' is the VALUE itself (e.g., "red")
  console.log("2.", color);
}
```

**Explanation:**

  * The `for...of` loop is much more readable. It says, "For each `color` *of* the `colors` array, run this block."
  * It automatically gives you the *value* (`"red"`, then `"green"`, then `"blue"`) without you needing to manage `i` or use `colors[i]`.

-----

## 🟣 Section 5: Loop Control Statements

Sometimes you need to change a loop's behavior *after* it has started.

### 1\. `break` (To Exit Immediately)

The `break` keyword **exits the loop entirely**, regardless of the loop's condition.

```javascript
// 1. 'break' - Find the *first* "admin" in a list
const users = ["guest", "editor", "admin", "moderator"];

console.log("1. 'break' example: Searching for admin...");

for (const user of users) {
  console.log("1. Checking:", user);
  if (user === "admin") {
    console.log("1. Found admin! Stopping the loop.");
    break; // EXIT the 'for' loop now.
  }
}
```

**Explanation:** The loop checks `"guest"`, then `"editor"`. Then it checks `"admin"`. The `if` statement is `true`, it prints "Found admin\!", and the `break` keyword immediately stops the loop. It **never** checks `"moderator"`.

### 2\. `continue` (To Skip an Iteration)

The `continue` keyword **skips the rest of the current iteration** and moves directly to the *next* one.

```javascript
// 2. 'continue' - Print only the even numbers
console.log("2. 'continue' example: Printing evens...");

for (let i = 0; i < 10; i++) {
  // Check if 'i' is an odd number
  if (i % 2 !== 0) { // '%' is the modulo operator (remainder)
    continue; // This number is odd. SKIP this iteration.
  }

  // This line is only reached if 'continue' was not run.
  console.log("2. Even number:", i);
}
```

**Explanation:**

  * **i = 0:** `(0 % 2 !== 0)` is `false`. Prints 0.
  * **i = 1:** `(1 % 2 !== 0)` is `true`. `continue` runs. The `console.log` is **skipped**. The loop moves to the increment (`i++`).
  * **i = 2:** `(2 % 2 !== 0)` is `false`. Prints 2.
  * **i = 3:** `(3 % 2 !== 0)` is `true`. `continue` runs. The `console.log` is **skipped**.

-----

## 📊 Quick Summary Table

| Loop Type | Syntax | Best For... | Runs At Least Once? |
| :--- | :--- | :--- | :--- |
| **`for`** | `for (let i=0; i<N; i++)` | When you know the number of iterations (e.g., 10 times). | No |
| **`while`** | `while (condition)` | When you only have a condition (e.g., `while (userIsLoggedIn)`). | No |
| **`do...while`**| `do { } while (condition)` | When you need the loop body to run at least one time. | **Yes** |
| **`for...of`** | `for (const item of array)` | The simplest way to loop through all items in an array. | No |
