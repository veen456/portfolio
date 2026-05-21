---
layout: post 
title: Data Types
hide: true
permalink: /data-types
show_reading_time: false
---

## Numbers

What are numbers?

Numbers are numerical values used for counting, measurements, and calculations. JavaScript supports both whole numbers (integers) and decimal numbers (floats).

Benefits of using numbers?

- Track game scores and health points
- Store positions and coordinates
- Perform mathematical calculations
- Handle timing and animations
- Manage game parameters and settings

```javascript
const playerHealth = 100;
const playerScore = 2500;
const playerX = 150.5;
const playerY = 300.75;

// Basic arithmetic
const totalScore = playerScore + 500;
const damage = playerHealth - 25;
const multiplier = playerScore * 2;
const halfDamage = 50 / 2;
const remainder = 10 % 3;

console.log("Score: " + playerScore);
console.log("Position: " + playerX + ", " + playerY);
console.log("Health after damage: " + damage);

// Math methods
console.log(Math.round(playerY)); // 301
console.log(Math.floor(playerY)); // 300
console.log(Math.ceil(playerY)); // 301
console.log(Math.random()); // random 0-1
```

```javascript
// Distance calculation and more advanced math
const player = { x: 100, y: 100 };
const target = { x: 300, y: 150 };

const dx = target.x - player.x;
const dy = target.y - player.y;
const distance = Math.sqrt(dx * dx + dy * dy);

console.log("Distance: " + distance);

// Percentage and scaling
const maxHealth = 100;
const currentHealth = 75;
const healthPercent = (currentHealth / maxHealth) * 100;

console.log("Health: " + healthPercent + "%");

// Clamping values
function clamp(value, min, max) {
    if (value < min) return min;
    if (value > max) return max;
    return value;
}

const playerX = 500;
const screenWidth = 800;
const clampedX = clamp(playerX, 0, screenWidth);
```

What does this code do?

- Calculates distance using Pythagorean theorem with `Math.sqrt()`
- Computes percentage of health remaining
- Creates `clamp()` function to keep values within a range
- Essential math operations used constantly in games
- Shows how to handle positions, health bars, and boundaries

---

## Strings

What are strings?

Strings are text data - letters, numbers, symbols, and spaces wrapped in quotes. They're one of the most common data types you'll use when working with user input, messages, and game data.

Benefits of using strings?

- Store and display text messages
- Work with user input and player names
- Create dynamic game dialogs and notifications
- Combine data together (concatenation)
- Parse and process textual information

```javascript
const playerName = "Astro";
const message = "Welcome to the game!";
const greeting = 'Hello!';

// String concatenation
const fullMessage = playerName + " says: " + message;
console.log(fullMessage);

// String properties
console.log(playerName.length); // 5
console.log(message.toUpperCase()); // WELCOME TO THE GAME!
console.log(message.toLowerCase()); // welcome to the game!
console.log(message.includes("game")); // true
console.log(message.charAt(0)); // W

// Template literals
const levelName = "Alien Planet";
const description = `You are on the ${levelName}. Stay alert!`;
console.log(description);
```

What does this code do?

- Creates three strings with different values and quote styles
- Combines strings using the `+` operator (concatenation)
- Uses `.length` to count characters
- Uses `.toUpperCase()` and `.toLowerCase()` to change case
- Uses `.includes()` to check if text is in the string
- Uses `.charAt()` to get a specific character
- Uses template literals with `${}` to embed variables

---

## Booleans

What are booleans?

Booleans are values that are either `true` or `false`. They're the simplest data type but incredibly important for making decisions and controlling program flow.

Benefits of using booleans?

- Make yes/no decisions in your code
- Control whether code runs or not
- Track states (is player alive? is button pressed?)
- Combine conditions with logic operators
- Essential for all conditional logic

```javascript
const isPlayerAlive = true;
const isGameOver = false;
const hasCollectible = true;

// Comparison operators
const playerHealth = 50;
const maxHealth = 100;

console.log(playerHealth > 0); // true
console.log(playerHealth === maxHealth); // false
console.log(playerHealth < maxHealth); // true
console.log(playerHealth <= 50); // true

// Logical operators
const hasShield = true;
const canMove = true;

console.log(hasShield && canMove); // true
console.log(hasShield || isGameOver); // true
console.log(!isGameOver); // true

// Using in code
if (isPlayerAlive && playerHealth > 0) {
    console.log("Player is still in the game!");
}
```

What does this code do?

- Combines multiple conditions with `&&` and `!` operators
- Stores boolean results in variables for reuse
- Uses `canShoot` to check multiple requirements before allowing action
- Loops through enemies and checks `alive` boolean for each
- Shows practical game logic: only alive enemies are processed
- Demonstrates how booleans control program flow

---

## Arrays

What are arrays?

Arrays are a way to store multiple values in a single variable. Instead of creating separate variables for each value, you can group them together in an ordered list.

Benefits of using arrays?

- Store multiple values with one variable name
- Access values by their position (index)
- Easier to loop through related data
- Keep code organized and scalable
- Work well with game objects and collections

```javascript
// Creating and using arrays
const gameObjects = ['player', 'guard', 'npc', 'background'];

// Accessing array elements
console.log(gameObjects[0]); // player
console.log(gameObjects[2]); // npc

// Adding items
gameObjects.push('collectible');

// Getting length
console.log(gameObjects.length); // 5

// Looping through array
for (let i = 0; i < gameObjects.length; i++) {
    console.log(gameObjects[i]);
}

// Using forEach method
gameObjects.forEach(item => {
    console.log("Item: " + item);
});
```

What does this code do?

- Creates an array with 4 game object names
- Accesses individual items using index notation (0 = first item)
- Uses `push()` to add a new item to the end
- Gets the `length` property to count items
- Loops through each item with a `for` loop
- Uses `forEach()` method to run code for each item

---

## Objects (JSON)

What are objects?

Objects are collections of properties (key-value pairs) grouped together. They let you organize related data and represent real-world entities like game characters, items, or settings.

Benefits of using objects?

- Organize related data together
- Access data using descriptive property names
- Represent complex entities (characters, items, etc.)
- Pass multiple related values efficiently
- Structure data in a readable way

```javascript
const player = {
    name: "Astro",
    health: 100,
    score: 0,
    position: { x: 100, y: 300 },
    inventory: ["shield", "weapon"]
};

// Accessing properties
console.log(player.name); // Astro
console.log(player.health); // 100
console.log(player.position.x); // 100
console.log(player.inventory[0]); // shield

// Modifying properties
player.health -= 20;
player.score += 100;

// Adding new properties
player.level = 1;

// Using in functions
function displayPlayer(character) {
    console.log(character.name + " has " + character.health + " health");
}
```

What does this code do?

- Creates an object with multiple properties
- Objects can contain nested objects and arrays
- Accesses properties using dot notation
- Modifies property values
- Adds new properties to existing object
- Passes objects to functions
