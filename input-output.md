---
layout: post 
title: Input/Output
hide: true
permalink: /input-output
show_reading_time: false
---

## Keyboard Input

What is keyboard input handling?

Keyboard input handling lets your program respond when the user presses keys. You can detect key presses and trigger code accordingly.

Benefits of keyboard input?

- Respond to player actions
- Build interactive games and applications
- Create real-time control systems
- Handle multiple keys simultaneously
- Build responsive user interfaces

```javascript
// Listening to keyboard events
let keysPressed = {};

document.addEventListener('keydown', function(event) {
    keysPressed[event.key] = true;
});

document.addEventListener('keyup', function(event) {
    keysPressed[event.key] = false;
});

// Check if specific key is pressed
function checkInput() {
    if (keysPressed['ArrowLeft']) {
        console.log("Moving left");
    }
    if (keysPressed['ArrowRight']) {
        console.log("Moving right");
    }
}
```

What does this code do?

- Listens for `keydown` events when key is pressed
- Listens for `keyup` events when key is released
- Stores key states in `keysPressed` object
- `checkInput()` can check which keys are currently pressed
- Allows detecting multiple simultaneous key presses

```javascript
// Movement system using keyboard input
let playerX = 100;
let playerY = 300;

document.addEventListener('keydown', function(event) {
    if (event.key === 'ArrowUp' || event.key === 'w') playerY -= 10;
    if (event.key === 'ArrowDown' || event.key === 's') playerY += 10;
    if (event.key === 'ArrowLeft' || event.key === 'a') playerX -= 10;
    if (event.key === 'ArrowRight' || event.key === 'd') playerX += 10;
    
    console.log("Player at (" + playerX + ", " + playerY + ")");
});
```

What does this code do?

- Detects arrow keys or WASD keys
- Updates player position based on key pressed
- Shows practical game movement system
- Handles multiple key mappings (arrows or WASD)
- Demonstrates real-time input handling for games

---

## Canvas Rendering

What is canvas rendering?

Canvas rendering uses the HTML5 Canvas API to draw graphics, sprites, and animations directly on the screen.

Benefits of canvas rendering?

- Draw custom graphics
- Create game visuals
- Render animations
- Display complex graphics
- Build interactive visuals

```javascript
// Get canvas and context
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

// Draw background
ctx.fillStyle = '#1a1a2e';
ctx.fillRect(0, 0, canvas.width, canvas.height);

// Draw player (rectangle)
ctx.fillStyle = '#00ff00';
ctx.fillRect(100, 300, 50, 50);

// Draw enemy (rectangle)
ctx.fillStyle = '#ff0000';
ctx.fillRect(200, 300, 50, 50);

// Draw circle
ctx.fillStyle = '#ffff00';
ctx.beginPath();
ctx.arc(150, 150, 30, 0, Math.PI * 2);
ctx.fill();
```

What does this code do?

- Gets canvas element and 2D drawing context
- Draws background rectangle
- Draws player as green rectangle
- Draws enemy as red rectangle
- Draws yellow circle
- Shows basic canvas drawing operations

```javascript
// Draw a complete game scene
function drawGameScene(ctx, canvas) {
    // Draw background
    const gradient = ctx.createLinearGradient(0, 0, canvas.width, canvas.height);
    gradient.addColorStop(0, '#1a1a2e');
    gradient.addColorStop(1, '#16213e');
    ctx.fillStyle = gradient;
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    
    // Draw game objects
    const gameObjects = [
        { x: 100, y: 300, size: 50, color: '#00ff00' },
        { x: 200, y: 300, size: 50, color: '#ff0000' }
    ];
    
    gameObjects.forEach(obj => {
        ctx.fillStyle = obj.color;
        ctx.fillRect(obj.x, obj.y, obj.size, obj.size);
    });
    
    // Draw text
    ctx.fillStyle = '#ffffff';
    ctx.font = '20px Arial';
    ctx.fillText('Game Running', 10, 30);
}
```

What does this code do?

- Creates gradient background for canvas
- Draws multiple game objects using loop
- Sets fill styles for colors
- Renders rectangles and text
- Shows complete game scene rendering
- Demonstrates multiple canvas drawing techniques together

---

## Game Environment Configuration

What is game environment configuration?

Game environment configuration sets up the initial parameters and properties for your game engine, including canvas size, assets, and settings.

Benefits of game environment configuration?

- Set game dimensions
- Configure asset paths
- Initialize game settings
- Set up game objects
- Prepare rendering environment

```javascript
// Game environment configuration
const gameEnv = {
    // Canvas settings
    innerWidth: 800,
    innerHeight: 600,
    path: "/path/to/game",
    
    // Asset paths
    imagePath: "/images/gamebuilder",
    spriteSheet: "/images/gamebuilder/sprites/astro.png",
    
    // Game settings
    SCALE_FACTOR: 5,
    STEP_FACTOR: 1000,
    ANIMATION_RATE: 50,
    
    // Initial objects
    objects: [
        { type: "player", x: 100, y: 300 },
        { type: "npc", x: 300, y: 300 }
    ]
};

console.log("Game configured:", gameEnv);
```

What does this code do?

- Sets game canvas dimensions
- Configures asset file paths
- Sets rendering parameters like scale and animation rate
- Lists initial game objects
- Centralizes all configuration in one object
- Makes configuration easy to modify

```javascript
// Advanced configuration from collisions-mechanic
const advancedGameEnv = {
    // Canvas
    innerWidth: 800,
    innerHeight: 600,
    path: "/projects/collisions-mechanic",
    
    // Player configuration
    player: {
        SCALE_FACTOR: 5,
        ANIMATION_RATE: 50,
        INIT_POSITION: { x: 100, y: 300 },
        keypress: { up: 87, left: 65, down: 83, right: 68 }
    },
    
    // Enemy configuration
    enemy: {
        SCALE_FACTOR: 8,
        ANIMATION_RATE: 50,
        INIT_POSITION: { x: 200, y: 300 }
    },
    
    // Difficulty settings
    difficulty: 'normal',
    difficulty_settings: {
        easy: { enemySpeed: 2, enemyHealth: 25 },
        normal: { enemySpeed: 4, enemyHealth: 50 },
        hard: { enemySpeed: 6, enemyHealth: 100 }
    }
};
```

What does this code do?

- Organizes configuration by component (player, enemy)
- Includes difficulty levels with different settings
- Centralizes all game parameters
- Makes it easy to adjust difficulty
- Shows nested configuration structure
- Demonstrates production-level game configuration

---

## API Integration

What is API integration?

API integration connects your game to external servers to fetch data, save progress, and communicate with other systems.

Benefits of API integration?

- Fetch game data from servers
- Save player progress
- Load levels and configurations
- Get real-time data
- Enable multiplayer features

```javascript
// Fetch game level data from API
async function loadLevel(levelId) {
    try {
        // Request level data
        const response = await fetch(`/api/levels/${levelId}`);
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const levelData = await response.json();
        
        // Initialize level with data
        console.log("Level loaded:", levelData);
        return levelData;
    } catch (error) {
        console.error("Failed to load level:", error);
    }
}

// Save player progress
async function saveProgress(playerId, progress) {
    await fetch(`/api/players/${playerId}/progress`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(progress)
    });
}
```

What does this code do?

- Fetches level data from API endpoint
- Checks if response is successful
- Parses JSON response
- Handles errors gracefully
- Saves player progress to server
- Shows both reading and writing API data

```javascript
// Complete game data lifecycle
async function initializeGame(playerId) {
    try {
        // Load player profile
        const playerData = await fetch(`/api/players/${playerId}`)
            .then(r => r.json());
        
        // Load current level
        const levelData = await fetch(`/api/levels/${playerData.currentLevel}`)
            .then(r => r.json());
        
        // Load player inventory
        const inventoryData = await fetch(`/api/players/${playerId}/inventory`)
            .then(r => r.json());
        
        // Initialize game with all data
        const gameState = {
            player: playerData,
            level: levelData,
            inventory: inventoryData,
            startTime: Date.now()
        };
        
        return gameState;
    } catch (error) {
        console.error("Game initialization failed:", error);
        return null;
    }
}
```

What does this code do?

- Loads player profile from API
- Loads level data based on player's current level
- Loads player inventory
- Combines all data into single game state
- Records game start time
- Shows complete game initialization workflow

---

## Asynchronous I/O

What is asynchronous I/O?

Asynchronous I/O allows your program to continue running while waiting for operations like loading files or fetching from APIs to complete, instead of stopping and waiting for them to finish.

Benefits of asynchronous I/O?

- Program doesn't freeze while waiting for data
- Handle multiple requests simultaneously
- Improve application responsiveness
- Better performance for network requests
- Essential for modern web applications

```javascript
// Modern async/await approach
async function loadGameState() {
    try {
        // Simulate fetching level data
        const levelResponse = await fetch('/api/levels/1');
        const levelData = await levelResponse.json();
        
        // Simulate fetching player data
        const playerResponse = await fetch('/api/player');
        const playerData = await playerResponse.json();
        
        // Combine data
        const gameState = {
            level: levelData,
            player: playerData
        };
        
        console.log("Game state loaded:", gameState);
        return gameState;
    } catch (error) {
        console.error("Failed to load game state:", error);
    }
}

// Call async function
loadGameState();
```

What does this code do?

- Defines asynchronous function that takes a callback
- Uses `setTimeout` to simulate delayed operation
- Continues executing without blocking
- Calls callback when operation completes
- Callback receives the loaded data
- Shows basic asynchronous pattern

---

## JSON Parsing

What is JSON parsing?

JSON parsing converts text (JSON format) into JavaScript objects. This lets you work with data received from servers, files, or APIs.

Benefits of JSON parsing?

- Convert text to usable objects
- Receive data from web servers
- Store and load game data
- Work with APIs
- Share data between programs

```javascript
// JSON to object
const jsonString = '{"name": "Guard", "health": 100, "level": 5}';
const gameData = JSON.parse(jsonString);

console.log(gameData.name); // Guard
console.log(gameData.health); // 100

// Object to JSON
const player = {
    name: "Astro",
    health: 100,
    level: 10
};

const jsonData = JSON.stringify(player);
console.log(jsonData); // {"name":"Astro","health":100,"level":10}
```

What does this code do?

- `JSON.parse()` converts text to JavaScript object
- Can now access properties like regular objects
- `JSON.stringify()` converts object back to text
- Useful for storing and sending data
- Both are essential for working with APIs and files

```javascript
// Parsing array of game objects
const gameDataJson = '[{"type":"guard","x":200,"y":100},{"type":"npc","x":300,"y":150}]';
const gameObjects = JSON.parse(gameDataJson);

gameObjects.forEach(obj => {
    console.log(obj.type + " at (" + obj.x + ", " + obj.y + ")");
});
```

What does this code do?

- Parses JSON array containing game objects
- Converts text into usable JavaScript array
- Loops through parsed objects
- Shows how to work with data from servers
- Demonstrates JSON parsing with complex data structures
