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

```javascript
// Real-world game math examples
function calculateDistance(x1, y1, x2, y2) {
    // Distance formula: √((x2-x1)² + (y2-y1)²)
    let dx = x2 - x1;
    let dy = y2 - y1;
    return Math.sqrt(dx * dx + dy * dy);
}

function clamp(value, min, max) {
    // Keep value between min and max
    return Math.max(min, Math.min(max, value));
}

function randomRange(min, max) {
    // Random integer between min and max
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Usage in game
let playerX = 100, playerY = 300;
let enemyX = 200, enemyY = 350;
let distance = calculateDistance(playerX, playerY, enemyX, enemyY);

let playerHealth = 150;
let damageReduction = 25;
playerHealth = clamp(playerHealth - damageReduction, 0, 100);

let randomScore = randomRange(10, 100);
```

What does this code do?

- `calculateDistance()` uses Pythagorean theorem for collision detection
- `clamp()` keeps values within acceptable ranges
- `randomRange()` generates random integers for game events
- Shows practical math functions used in games
- Demonstrates combining multiple operators in calculations
- Real-world examples of mathematical operators in game development

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

```javascript
// Advanced string operations
let itemList = "sword,shield,potion,bow";

// Split and join for data conversion
let items = itemList.split(","); // ["sword", "shield", "potion", "bow"]
console.log(items[0]); // sword
console.log(items.join(" | ")); // sword | shield | potion | bow

// String manipulation for formatting
function formatPlayerStats(name, health, level) {
    return name.toUpperCase() + " - Health: " + health + " Level: " + level;
}

let stats = formatPlayerStats("astro", 100, 5);
console.log(stats); // ASTRO - Health: 100 Level: 5

// Search and extract
let fullName = "Guard_Patrol_001";
if (fullName.includes("Guard")) {
    console.log("This is a guard unit");
}

let index = fullName.indexOf("Patrol");
let guardType = fullName.substring(0, index - 1);
console.log(guardType); // Guard
```

What does this code do?

- `.split()` breaks string into array using delimiter
- `.join()` combines array into string with separator
- Shows formatting strings for display
- `.includes()` and `.indexOf()` find text patterns
- `.substring()` extracts specific portions
- Demonstrates data processing with strings
- Real-world parsing and formatting examples

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
// Comparison operators
let playerHealth = 50;
let enemyHealth = 30;

console.log(playerHealth > enemyHealth); // true (greater than)
console.log(playerHealth < enemyHealth); // false (less than)
console.log(playerHealth === 50); // true (equal to)
console.log(playerHealth !== 100); // true (not equal to)
console.log(playerHealth >= 50); // true (greater than or equal)
console.log(playerHealth <= 100); // true (less than or equal)

// Logical operators combining conditions
let hasAmmo = true;
let targetInRange = true;

console.log(hasAmmo && targetInRange); // true (AND - both true)
console.log(hasAmmo || false); // true (OR - at least one true)
console.log(!hasAmmo); // false (NOT - opposite)
```

What does this code do?

- Comparison operators (>, <, ===, !==, >=, <=) check values
- && (AND) requires both conditions true
- || (OR) requires at least one condition true
- ! (NOT) reverses boolean value
- Essential for if statements and game logic
- Shows how to combine multiple conditions

```javascript
// Complex boolean expressions in game logic
let playerHealth = 100;
let playerAmmo = 5;
let isReloading = false;
let targetInRange = true;
let hasLineOfSight = true;

// Can player shoot?
if (playerAmmo > 0 && !isReloading && targetInRange && hasLineOfSight) {
    console.log("Fire!");
    playerAmmo--;
}

// Is player safe to move?
if (playerHealth > 25 || (playerAmmo > 0 && targetInRange === false)) {
    console.log("Moving to new position");
}

// Complex condition combining AND/OR
let canAttack = (playerHealth > 50 && playerAmmo >= 3) || (playerHealth > 75 && playerAmmo > 0);
if (canAttack) {
    console.log("Attack!");
}

// Nested conditions
let levelComplete = false;
let allEnemiesDead = true;
let allObjectivesMetup = true;

if (allEnemiesDead && allObjectivesMetup) {
    levelComplete = true;
    console.log("Level won!");
}
```

What does this code do?

- Combines multiple conditions with && and ||
- Uses ! to invert conditions
- Shows practical game logic decisions
- Demonstrates complex boolean expressions
- Shows how conditions control game flow
- Real-world examples of conditional game mechanics
