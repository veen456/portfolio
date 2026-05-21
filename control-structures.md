---
layout: post 
title: Control Structures
hide: true
permalink: /control-structures
show_reading_time: false
---

## Iteration (Loops)

What is iteration?

Iteration means repeating code multiple times using loops. Instead of writing the same code over and over, you can use a loop to run it as many times as needed.

Benefits of iteration?

- Repeat actions without duplicating code
- Process all items in an array or list
- Handle repetitive tasks automatically
- Update game objects every frame
- Scale to handle any number of items

```javascript
// for loop
for (let i = 0; i < 5; i++) {
    console.log("Loop iteration: " + i);
}

// while loop
let count = 0;
while (count < 3) {
    console.log("Count: " + count);
    count++;
}

// forEach
const gameObjects = ['player', 'guard', 'npc'];
gameObjects.forEach(function(object) {
    console.log("Updating: " + object);
});

// for...of loop
for (const object of gameObjects) {
    console.log("Object: " + object);
}
```

What does this code do?

- Uses `for` loop to run code exactly 5 times
- Uses `while` loop to repeat while condition is true
- Uses `forEach()` to run function for each array item
- Uses `for...of` loop for cleaner array iteration
- Shows different loop styles for different situations

```javascript
// Practical example: update all game objects
const objects = [
    { name: 'player', x: 100 },
    { name: 'guard', x: 200 },
    { name: 'npc', x: 300 }
];

for (let obj of objects) {
    obj.x += 5; // Move each object right
    console.log(obj.name + " moved to " + obj.x);
}
```

What does this code do?

- Updates each object in the array one by one
- Uses `for...of` to iterate through the array
- Modifies each object's position by adding 5
- Shows how iteration is essential for game updates
- Processes all game objects in a single loop

---

## Conditionals

What are conditionals?

Conditionals are statements that run different code based on whether a condition is true or false. They let your program make decisions and respond to different situations.

Benefits of conditionals?

- Make decisions based on game state
- Control different behaviors for different situations
- Handle player input and respond appropriately
- Check errors and handle problems
- Create dynamic, responsive programs

```javascript
const playerHealth = 50;

if (playerHealth <= 0) {
    console.log("Game Over!");
}

// if...else
if (playerHealth > 75) {
    console.log("Player is healthy!");
} else {
    console.log("Player needs healing!");
}

// if...else if...else
const levelScore = 2500;

if (levelScore >= 5000) {
    console.log("Gold medal!");
} else if (levelScore >= 3000) {
    console.log("Silver medal!");
} else if (levelScore >= 1000) {
    console.log("Bronze medal!");
} else {
    console.log("Try again!");
}

// switch
const playerAction = "jump";
switch (playerAction) {
    case "jump":
        console.log("Player jumps!");
        break;
    case "run":
        console.log("Player runs!");
        break;
    default:
        console.log("Unknown action");
}
```

What does this code do?

- Uses nested `if` statements to check conditions in sequence
- Only checks next condition if previous one was true
- Shows practical game logic: player must be alive AND have weapon AND target in range to attack
- Each level of nesting adds another requirement
- Demonstrates hierarchical decision-making
- Real-world example: how games control what players can do

---

## Nested Conditionals

What are nested conditionals?

Nested conditionals are `if` statements inside other `if` statements. They let you check conditions based on the results of previous conditions.

Benefits of nested conditionals?

- Handle complex decision trees
- Only check certain conditions when others are true
- Create multi-level game logic
- Reduce unnecessary checks
- Build hierarchical decision structures

```javascript
const playerHealth = 50;
const hasWeapon = true;
const targetDistance = 5;
const weaponRange = 10;

if (playerHealth > 0) {
    console.log("Player is alive");
    
    if (hasWeapon) {
        console.log("Player has a weapon");
        
        if (targetDistance <= weaponRange) {
            console.log("Target is in range!");
            console.log("ATTACK!");
        } else {
            console.log("Target is too far away");
        }
    } else {
        console.log("Player has no weapon");
    }
} else {
    console.log("Player is dead");
}
```

What does this code do?

- First `if` checks if player is alive
- Inside that, second `if` checks if player has weapon
- Inside that, third `if` checks if target is in range
- Each level only runs if all previous conditions were true

```javascript
// Game state logic
const isPlaying = true;
const isPaused = false;

if (isPlaying) {
    if (!isPaused) {
        console.log("Game is running - update game objects");
    } else {
        console.log("Game is paused");
    }
}
```

What does this code do?

- First checks if game is playing
- Then checks if game is NOT paused
- Only runs game update code if both conditions are true
- Shows practical game state management
- Prevents updates when game is paused or not running

