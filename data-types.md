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
class WaveManager {
    constructor(gameEnv) {
        this.gameEnv = gameEnv;
        this.waves = [
            { count: 5,  speed: 1.5  },  // Wave 1
            { count: 9, speed: 2.5  },  // Wave 2
            { count: 17,speed: 3.5  }   // Wave 3
        ];

        this.currentWave = 0;
        this.waveEnemies = [];
        this.waveActive = false;
        this.waveStartTime = 0;
        this.npcSpawned = false;
        this._playerDead = false;

        // Projectile system
        this.projectiles = [];
        this.lastAttackTime = Date.now();
        this.attackCooldown = 250; // 0.25s between shots

```

What does this code do?
- The numbers for each wave represent how many enemies there are and their velocity.
- Both of these aspects are controlled by numbers
- The player attack cooldown is also controlled by numbers (250 milliseconds or 0.25 second shot cooldown)
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
winLevel() {
        if (this.levelWon) return;
        this.levelWon = true;

        console.log("🎉 Level 4 Won!");

        const dialogueSystem = new DialogueSystem();
        dialogueSystem.showDialogue(
            'You have defeated all waves! You are a true warrior!',
            'Victory!',
            this.gameEnv.path + '/images/projects/mansionGame/key_lvl3.png'
        );
```

What does this code do?

- We use a string to type to the console is the player has won the game
- Strings use quotation marks to define themselves from other data types

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

### Common Array Functions

| Function | Purpose | Example |
|----------|---------|---------|
| **push()** | Adds element to the end | `arr.push(5)` |
| **pop()** | Removes last element | `arr.pop()` |
| **length** | Gets number of elements | `arr.length` |
| **[index]** | Access element by position | `arr[0]` gets first item |
| **forEach()** | Loop through each element | `arr.forEach(x => console.log(x))` |
| **map()** | Transform each element | `arr.map(x => x * 2)` |
| **filter()** | Select elements that match | `arr.filter(x => x > 5)` |
| **indexOf()** | Find position of element | `arr.indexOf(5)` |

Benefits of using arrays?

- Store multiple values with one variable name
- Access values by their position (index)
- Easier to loop through related data
- Keep code organized and scalable
- Work well with game objects and collections

```javascript
// Creating and using arrays
const playerStartX = width * 0.1;
const playerStartY = height / 2;
const minSpawnDist = Math.min(width, height) * 0.5;
const minGhostSpacing = 150; // Minimum distance between ghosts

const spawnedPositions = []; // Track all spawned ghost positions

for (let i = 0; i < count; i++) {
    let xPos, yPos;
    let validSpawn = false;
    // Loop continues to spawn ghosts at valid positions
    spawnedPositions.push({x: xPos, y: yPos}); // Add position to array
}
```

What does this code do?

- Creates an empty array called `spawnedPositions` to store ghost positions
- Uses a `for` loop to iterate and create multiple ghost spawn positions
- Adds each new position object to the array using the `push()` method
- Each position is stored in order, allowing you to access them later by index
- The array grows dynamically as new positions are added
- This pattern is useful for tracking collections of game objects

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
const image_data_background = {
    name: 'background',
    greeting: "Wave Defense! Defeat all enemies to proceed!",
    src: path + "/images/projects/mansionGame/lvl4.png",
    pixels: { height: 1600, width: 1600 }
};

// Player
const sprite_data_player = {
    id: 'Spook',
    greeting: "Hi, I am Spook.",
    src: path + "/images/projects/mansionGame/spookMcWalk.png",
    SCALE_FACTOR: 6,
    STEP_FACTOR: 500,
    ANIMATION_RATE: 10,
    INIT_POSITION: { x: width * 0.1, y: height / 2 },
    pixels: { height: 2400, width: 3600 },
    orientation: { rows: 2, columns: 3 },
    down:      { row: 1, start: 0, columns: 3 },
    downRight: { row: 1, start: 0, columns: 3, rotate:  Math.PI / 16 },
    downLeft:  { row: 0, start: 0, columns: 3, rotate: -Math.PI / 16 },
    left:      { row: 0, start: 0, columns: 3 },
    right:     { row: 1, start: 0, columns: 3 },
    up:        { row: 1, start: 0, columns: 3 },
    upLeft:    { row: 0, start: 0, columns: 3, rotate:  Math.PI / 16 },
    upRight:   { row: 1, start: 0, columns: 3, rotate: -Math.PI / 16 },
    hitbox: { widthPercentage: 0.45, heightPercentage: 0.2 },
    keypress: { up: 87, left: 65, down: 83, right: 68 } // W A S D
};
```

What does this code do?

- The `image_data_background` object stores metadata about the game background image as key-value pairs
- The `pixels` property contains a nested object that holds the image dimensions
- The `sprite_data_player` object stores all the configuration data for a player character in one place
- Nested objects like `INIT_POSITION`, `pixels`, and `orientation` organize related data together
- Direction objects (`down`, `left`, `right`, etc.) contain animation frame data for each movement direction
- The `keypress` property maps keyboard keys (by code) to movement directions
- Accessing properties is done with dot notation: `sprite_data_player.id` returns `'Spook'`
- This pattern keeps related data organized and makes code more maintainable

