---
layout: post 
title: Debugging
hide: true
permalink: /debugging
show_reading_time: false
---

## Console Debugging

What is console debugging?

Console debugging uses `console.log()` and similar functions to print values and track program execution. It's the simplest way to see what your code is doing.

Benefits of console debugging?

- View variable values
- Track program flow
- Identify where code fails
- Simple and always available
- Quick debugging method

```javascript
// Console debugging methods
const player = { name: "Astro", health: 100 };
const enemy = { name: "Guard", health: 50 };

console.log("Player:", player);
console.log("Enemy health:", enemy.health);

// Log with label
console.log("Game state:", { player, enemy });

// Warning message
console.warn("Low health!");

// Error message
console.error("Player took too much damage!");
```

What does this code do?

- Uses `console.log()` to print normal messages
- Uses `console.warn()` for warnings
- Uses `console.error()` for errors
- Can log objects and multiple values
- Shows output in browser console

---

## Hitbox Visualization

What is hitbox visualization?

Hitbox visualization displays collision boundaries on screen so you can see and debug collision detection in real-time.

Benefits of hitbox visualization?

- Debug collision detection
- Visualize hitbox boundaries
- Test collision accuracy
- Adjust hitbox size
- Improve collision logic

```javascript
// Draw hitboxes for debugging
function drawHitbox(ctx, object, debug = true) {
    if (!debug) return;
    
    // Draw transparent rectangle for hitbox
    ctx.strokeStyle = '#00ff00';
    ctx.lineWidth = 2;
    ctx.globalAlpha = 0.5;
    
    ctx.strokeRect(
        object.x,
        object.y,
        object.width,
        object.height
    );
    
    ctx.globalAlpha = 1.0;
    
    // Label the hitbox
    ctx.fillStyle = '#00ff00';
    ctx.font = '12px Arial';
    ctx.fillText(object.name, object.x, object.y - 5);
}

// Usage
const gameObjects = [
    { name: 'player', x: 100, y: 300, width: 50, height: 50 },
    { name: 'enemy', x: 200, y: 300, width: 50, height: 50 }
];

// Draw all hitboxes
gameObjects.forEach(obj => drawHitbox(ctx, obj, true));
```

What does this code do?

- Draws green rectangles around game objects
- Uses transparency for better visibility
- Labels each hitbox with object name
- Shows hitbox boundaries on canvas
- Helps debug collision detection
- Can be toggled on/off with debug flag

```javascript
// Collision detection with visual debugging
function checkCollision(obj1, obj2, ctx, debugDraw = true) {
    // Calculate collision
    const colliding = !(
        obj1.x + obj1.width < obj2.x ||
        obj1.x > obj2.x + obj2.width ||
        obj1.y + obj1.height < obj2.y ||
        obj1.y > obj2.y + obj2.height
    );
    
    // Debug visualization
    if (debugDraw) {
        const color = colliding ? '#ff0000' : '#00ff00';
        
        // Draw both objects
        ctx.strokeStyle = color;
        ctx.lineWidth = 3;
        ctx.strokeRect(obj1.x, obj1.y, obj1.width, obj1.height);
        ctx.strokeRect(obj2.x, obj2.y, obj2.width, obj2.height);
        
        // Draw collision info
        ctx.fillStyle = color;
        ctx.font = '14px Arial';
        if (colliding) {
            ctx.fillText('COLLISION!', 10, 20);
        }
    }
    
    return colliding;
}
```

What does this code do?

- Checks if two objects collide
- Draws red box if collision occurs, green if not
- Shows both object boundaries
- Displays "COLLISION!" text when objects touch
- Helps debug collision detection
- Shows visual debugging in action

---

## Source-Level Debugging

What is source level debugging?

Source level debugging uses browser developer tools to pause code execution, inspect variables, and step through code line by line.

Benefits of source level debugging?

- Pause execution at breakpoints
- Step through code line by line
- Inspect variable values while paused
- See call stack
- More powerful than console.log()

```javascript
// Set breakpoint by adding debugger statement
function movePlayer(x, y) {
    debugger; // Execution pauses here
    
    const newX = x + 10;
    const newY = y + 10;
    
    console.log("Player moved to: (" + newX + ", " + newY + ")");
    return { x: newX, y: newY };
}

// When function is called, execution pauses at debugger
const newPos = movePlayer(100, 300);
```

What does this code do?

- `debugger` statement pauses execution
- Can also set breakpoints in browser DevTools
- Pause lets you inspect variable values
- Can step through code line by line
- More powerful than console.log for debugging

```javascript
// Example with multiple breakpoints
function attackEnemy(enemyHealth, damage) {
    debugger; // First breakpoint
    
    let newHealth = enemyHealth - damage;
    
    debugger; // Second breakpoint
    
    if (newHealth <= 0) {
        console.log("Enemy defeated!");
    }
    
    return newHealth;
}

const result = attackEnemy(50, 30);
console.log("Result: " + result);
```

What does this code do?

- Sets multiple breakpoints in function
- Allows stepping through function execution
- Inspects variable values at each breakpoint
- Helps understand function flow
- More granular debugging than single breakpoint

---

## Network Debugging

What is network debugging?

Network debugging monitors requests and responses between your application and servers to identify communication problems.

Benefits of network debugging?

- See all network requests
- Check response status and data
- Identify failed requests
- Monitor performance
- Debug API issues

```javascript
// Fetch data from API
fetch('/api/game/level/1')
    .then(response => {
        // Check response status
        console.log("Response status:", response.status);
        
        if (!response.ok) {
            console.error("Request failed with status:", response.status);
        }
        
        return response.json();
    })
    .then(data => {
        console.log("Data received:", data);
    })
    .catch(error => {
        console.error("Network error:", error);
    });
```

What does this code do?

- Uses `fetch()` to request data from server
- Checks response status code
- Logs errors if request fails
- Parses JSON response
- Shows data received from server
- Handles network errors with catch block

```javascript
// Monitor multiple requests
async function loadGameData() {
    try {
        // Request 1: Load level data
        const levelResponse = await fetch('/api/level/1');
        console.log("Level response status:", levelResponse.status);
        const levelData = await levelResponse.json();
        
        // Request 2: Load player data
        const playerResponse = await fetch('/api/player');
        const playerData = await playerResponse.json();
        
        // Request 3: Load assets
        const assetsResponse = await fetch('/api/assets');
        const assetsData = await assetsResponse.json();
        
        console.log("All data loaded successfully");
        return { level: levelData, player: playerData, assets: assetsData };
    } catch (error) {
        console.error("Failed to load game data:", error);
    }
}
```

What does this code do?

- Uses `async/await` for cleaner request handling
- Makes three separate API requests
- Checks response status for each request
- Parses JSON from each response
- Combines all data into single object
- Catches and logs any network errors

---

## Application Debugging

What is application debugging?

Application debugging is fixing problems in your entire application by identifying where things go wrong and why.

Benefits of application debugging?

- Find and fix application-wide issues
- Understand unexpected behavior
- Improve application reliability
- Track down complex bugs
- Learn what went wrong

```javascript
// Track what's happening in the app
let gameRunning = true;
let playerHealth = 100;

// Log important events
console.log("Game started");

// Simulate damage
playerHealth -= 20;
console.log("Player health after damage: " + playerHealth);

// Check if critical
if (playerHealth < 30) {
    console.error("CRITICAL: Player health is low!");
}

// Check game status
if (gameRunning && playerHealth > 0) {
    console.log("Game continues - player alive");
} else {
    console.warn("Game may need to end");
}
```

What does this code do?

- Logs game start event
- Tracks player health changes
- Detects critical health situations
- Uses different log levels (log, warn, error)
- Shows how to monitor application state
- Helps identify where problems occur

```javascript
// Debug a game loop
function gameLoop() {
    // Track frame count
    console.log("Frame: " + frameCount);
    
    // Check for errors
    try {
        updateGame();
        renderGame();
    } catch (error) {
        console.error("Game loop error:", error);
        gameRunning = false;
    }
    
    // Performance tracking
    console.time('game_update');
    // ... game update code ...
    console.timeEnd('game_update');
}

// Profile memory usage
console.log("Memory:", performance.memory);
```

What does this code do?

- Logs frame count for performance tracking
- Wraps game code in try-catch for error handling
- Logs errors when they occur
- Uses `console.time()` and `console.timeEnd()` to measure performance
- Monitors memory usage
- Shows comprehensive application debugging techniques

---

## Element Inspection

What is element inspection?

Element inspection lets you examine and modify HTML elements on a web page in real-time using browser developer tools.

Benefits of element inspection?

- View and modify HTML structure
- Change CSS styles temporarily
- Inspect element properties
- Debug layout issues
- Test changes without code

```javascript
// Get HTML elements from the page
const gameCanvas = document.getElementById('gameCanvas');
const healthBar = document.querySelector('.health-bar');
const scoreDisplay = document.querySelector('.score');

// Inspect element properties
console.log("Canvas element:", gameCanvas);
console.log("Canvas width:", gameCanvas.width);
console.log("Canvas height:", gameCanvas.height);

// Modify elements
healthBar.style.backgroundColor = 'red';
scoreDisplay.textContent = '1000';

// Get all elements of a type
const buttons = document.querySelectorAll('button');
console.log("Number of buttons:", buttons.length);
```

What does this code do?

- Uses `getElementById()` to get elements by ID
- Uses `querySelector()` to get elements by CSS selector
- Accesses element properties like width and height
- Modifies element styles directly
- Modifies element content
- Uses `querySelectorAll()` to get multiple elements

```javascript
// Find and modify specific elements
const allDivs = document.querySelectorAll('div');

// Inspect each element
allDivs.forEach(div => {
    console.log("Div:", div.id, div.className);
    
    // Check computed styles
    const styles = window.getComputedStyle(div);
    console.log("Width:", styles.width);
    console.log("Background:", styles.backgroundColor);
});

// Add event listener for debugging
const button = document.querySelector('button');
button.addEventListener('click', function() {
    console.log("Button clicked!");
    console.log("Event target:", this);
});
```

What does this code do?

- Gets all div elements on page
- Logs each element's ID and class
- Inspects computed styles
- Checks actual width and background color
- Adds event listener to button
- Shows how to debug element interactions