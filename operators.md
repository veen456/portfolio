---
layout: post 
title: Operators
hide: true
permalink: /operators
show_reading_time: false
---

## Mathematical

What are mathematical operators?

Mathematical operators perform calculations on numbers. JavaScript supports standard math operations plus some advanced functions in the Math object.

Benefits of mathematical operators?

- Calculate positions and movement
- Handle damage and health calculations
- Manage scoring and resources
- Create physics and collision systems
- Process numerical game data

```javascript
// Basic mathematical operators
let x = 10;
let y = 5;

console.log(x + y); // 15 (addition)
console.log(x - y); // 5 (subtraction)
console.log(x * y); // 50 (multiplication)
console.log(x / y); // 2 (division)
console.log(x % y); // 0 (modulo/remainder)
console.log(x ** 2); // 100 (exponentiation)

// Math object methods
console.log(Math.max(10, 20, 5)); // 20
console.log(Math.min(10, 20, 5)); // 5
console.log(Math.random()); // random 0-1
console.log(Math.round(4.7)); // 5
console.log(Math.abs(-10)); // 10
console.log(Math.sqrt(25)); // 5
```

What does this code do?

- Demonstrates all basic mathematical operators (+, -, *, /, %, **)
- Shows Math object methods for finding max/min values
- Math.random() generates random numbers for games
- Math.round() rounds decimals to integers
- Math.abs() gets absolute value
- Math.sqrt() calculates square root
- Essential for game calculations
---

## String Operations

What are string operations?

String operations allow you to change strings by adding, removing, re-ordering, and more. They let you extract parts of strings, change formatting, search for text, and transform data.

Benefits of string operations?

- Process user input
- Extract and format data
- Search and replace text
- Validate and parse information
- Build dynamic messages and UI text

```javascript
// Common string methods
let playerName = "Astro";
let message = "Welcome to the game!";

// String properties and methods
console.log(playerName.length); // 5
console.log(playerName.toUpperCase()); // ASTRO
console.log(playerName.toLowerCase()); // astro
console.log(playerName.charAt(0)); // A (first character)
console.log(message.indexOf("game")); // 15 (position of word)
console.log(message.substring(0, 7)); // Welcome (extract part)
console.log(message.includes("game")); // true
console.log(message.replace("game", "adventure")); // Welcome to the adventure!
```

What does this code do?

- `.length` gets number of characters
- `.toUpperCase()` and `.toLowerCase()` change letter case
- `.charAt()` gets single character at position
- `.indexOf()` finds position of text
- `.substring()` extracts part of string
- `.includes()` checks if text contains substring
- `.replace()` swaps one text for another
- Essential for text manipulation
---

## Boolean Expressions

What are boolean expressions?

Boolean expressions are combinations of values and operators that result in true or false. They let you check complex conditions in your code.

Benefits of boolean expressions?

- Check multiple conditions at once
- Create complex game logic
- Combine comparisons
- Improve code readability
- Essential for decision-making in programs

```javascript
// Game scenario: Checking if player can attack
let playerHealth = 50;
let hasAmmo = true;
let targetInRange = true;
let isAlive = true;

// AND operator (&&) - ALL conditions must be true
console.log(hasAmmo && targetInRange); // true - player can attack
console.log(hasAmmo && targetInRange && isAlive); // true - all conditions met
console.log(hasAmmo && playerHealth > 0); // true - has ammo and alive

// OR operator (||) - AT LEAST ONE condition must be true
let hasWeapon = false;
let hasMagic = true;

console.log(hasWeapon || hasMagic); // true - player can attack with magic
console.log(playerHealth < 20 || hasAmmo === false); // false - player has health and ammo

// NOT operator (!) - Reverses/inverts the boolean
console.log(!isAlive); // false - player IS alive
console.log(!hasAmmo); // false - player DOES have ammo
console.log(!(playerHealth < 10)); // true - player health is NOT below 10

// Combining all three operators
let canAttack = hasAmmo && targetInRange && isAlive;
let shouldRun = playerHealth < 20 || hasAmmo === false;
let isSafe = !(playerHealth < 10 && targetInRange);

console.log(canAttack); // true - all conditions for attack are met
console.log(shouldRun); // false - player doesn't need to run
console.log(isSafe); // true - player is not in danger
```

What does this code do?

- **AND operator (&&)**: Checks if ALL conditions are true. `hasAmmo && targetInRange` only returns true if both are true
- **OR operator (||)**: Checks if AT LEAST ONE condition is true. `hasWeapon || hasMagic` returns true if player has either weapon or magic
- **NOT operator (!)**: Inverts/reverses a boolean. `!isAlive` returns the opposite of isAlive's value
- Game scenario: Player can only attack if they have ammo AND target is in range AND player is alive
- Shows practical decision-making: combining multiple conditions for game logic
- Essential for controlling complex game behavior based on multiple factors