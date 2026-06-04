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
syncPlayerMovementInput() {
    const player = this.getPlayer();
    if (!player || !player.pressedKeys) return;

    const movementKeys = [
        ['KeyW', player.keypress.up],
        ['KeyA', player.keypress.left],
        ['KeyS', player.keypress.down],
        ['KeyD', player.keypress.right]
    ];

    // Check which keys are pressed and move player accordingly
    movementKeys.forEach(([key, direction]) => {
        if (player.pressedKeys[key]) {
            player.move(direction);
        }
    });
}
```

What does this code do?

- Gets the current player object from the game
- Checks if the player and pressedKeys object exist before proceeding
- Creates an array mapping keyboard keys (W, A, S, D) to movement directions
- Loops through each key mapping using `forEach()`
- For each key, checks if it's currently being held down in the `pressedKeys` object
- If a key is pressed, calls the player's `move()` method with the corresponding direction
- Handles multiple simultaneous key presses (player can move diagonally)
- Separates input detection from movement logic for cleaner code

## Canvas Rendering

What is canvas rendering?

Canvas rendering uses code to draw a canvas with visuals and update it every frame, allowing for a game to start up and work, changing the screen every frame.

Benefits of canvas rendering?

- Draw custom graphics
- Create game visuals
- Render animations
- Display complex graphics
- Build interactive visuals

```javascript
draw() {
    this.clearCanvas();
    const ctx = this.ctx;
    const dstW = Math.max(1, Math.floor(this.canvas.width));
    const dstH = Math.max(1, Math.floor(this.canvas.height));

    ctx.save();
    ctx.translate(dstW / 2, dstH / 2);
    ctx.rotate(this.rotation);
    ctx.shadowColor = 'rgba(184, 242, 230, 0.75)';
    ctx.shadowBlur = 12;

    if (this.imageLoaded && this.spriteSheet?.complete) {
        ctx.drawImage(
            this.spriteSheet,
            0, 0, this.spriteSheet.naturalWidth, this.spriteSheet.naturalHeight,
            -dstW / 2, -dstH / 2, dstW, dstH
        );
    } else {
        ctx.fillStyle = '#B8F2E6';
        ctx.fillRect(-dstW / 2, -dstH / 8, dstW, dstH / 4);
    }

    ctx.restore();
    this.setupCanvas();
}
```

What does this code do?

- `clearCanvas()` removes everything drawn in the previous frame
- Gets the 2D canvas context (`ctx`) for drawing operations
- Calculates destination width and height, ensuring minimum value of 1 to prevent errors
- `ctx.save()` saves the current canvas state (styles, transformations) to a stack
- `ctx.translate()` moves the drawing origin to the center of the canvas
- `ctx.rotate()` rotates the sprite by the object's rotation angle
- Sets up shadow effects: `shadowColor` (cyan with transparency) and `shadowBlur` (12 pixels)
- If sprite image is loaded, uses `drawImage()` to draw the sprite sheet at the center position with proper scaling
- If sprite isn't loaded yet, draws a placeholder rectangle (fallback)
- `ctx.restore()` restores the previous canvas state, undoing the transformations
- `setupCanvas()` prepares the canvas for the next frame

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
 // Background configuration
const image_data_background = {
    name: 'background',
    greeting: "Wave Defense! Defeat all enemies to proceed!",
    src: path + "/images/projects/mansionGame/level4.png",
    pixels: { height: 1600, width: 1600 }
};

// Player sprite configuration
const sprite_data_player = {
    id: 'Spook',
    greeting: "You shouldn't be reading this.",
    src: path + "/images/projects/mansionGame/spookMcWalk.png",
    SCALE_FACTOR: 6,
    STEP_FACTOR: 500,
    ANIMATION_RATE: 11,
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

// Register game objects
this.classes = [
    { class: GameEnvBackground, data: image_data_background },
    { class: Player, data: sprite_data_player }
];
```
What does this code do?

- **Background configuration** stores metadata about the level background image including name, greeting message, image path, and pixel dimensions
- **Player configuration** (`sprite_data_player`) stores all the settings needed to create and animate the player character
- `id: 'Spook'` identifies the player sprite
- `src` points to the sprite sheet image file
- `SCALE_FACTOR: 6` controls how large the sprite is drawn on canvas
- `STEP_FACTOR: 500` controls movement speed (higher = slower)
- `ANIMATION_RATE: 11` controls how fast sprite animations play (frames per animation)
- `INIT_POSITION` sets where the player starts (10% from left, centered vertically)
- `pixels` stores the total sprite sheet dimensions (2400 x 3600)
- `orientation` defines the sprite sheet layout (2 rows, 3 columns of animation frames)
- Direction objects (`down`, `left`, `right`) specify which animation frame row and number of columns for each direction
- Some directions include `rotate` to tilt the sprite (e.g., diagonal movement uses rotation)
- `hitbox` defines collision area as a percentage of sprite size (45% width, 20% height)
- The `this.classes` array registers both game objects with their configuration data so the engine can initialize them

---

## API Integration

What is API integration?

API integration connects your game to external servers to fetch data, save progress, and communicate with other systems.
An API is an application programming interface

Benefits of API integration?

- Fetch game data from servers
- Save player progress
- Load levels and configurations
- Get real-time data
- Enable multiplayer features

```javascript
        // Background music from mansion game
        this.backgroundMusic = new Audio(path + '/assets/sounds/mansionGame/SpookieDookie.mp3');
        this.backgroundMusic.loop   = true;
        this.backgroundMusic.volume = 0.4;
        this.backgroundMusic.play();

        this.setupInputListener();
        this.showStartUI();
```
What does this code do?

- Uses the **Audio Web API** to integrate sound resources from an external file path
- `new Audio()` creates an audio object and uses the browser's API to handle loading the audio file asynchronously
- `path + '/assets/sounds/mansionGame/SpookieDookie.mp3'` specifies the resource location (like calling an API endpoint)
- `this.backgroundMusic.loop = true` configures the audio to repeat continuously
- `this.backgroundMusic.volume = 0.4` sets the volume level to 40% via the Audio API
- `this.backgroundMusic.play()` calls the API method to start audio playback
- This demonstrates API integration by fetching and controlling a resource (the audio file) from the server using the browser's built-in Web API
- The Audio API handles all the complexities of loading, decoding, and playing the file without blocking the game
- `this.setupInputListener()` and `this.showStartUI()` execute immediately while the audio loads asynchronously in the background
- This pattern is similar to how you'd fetch game data, save progress, or retrieve levels from a server using APIs

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
        // Background music from mansion game
        this.backgroundMusic = new Audio(path + '/assets/sounds/mansionGame/SpookieDookie.mp3');
        this.backgroundMusic.loop   = true;
        this.backgroundMusic.volume = 0.4;
        this.backgroundMusic.play();

        this.setupInputListener();
        this.showStartUI();
```

What does this code do?

- `new Audio()` creates an audio object and starts loading the sound file *asynchronously* in the background without blocking the program
- `this.backgroundMusic.loop = true` sets the audio to repeat when it finishes
- `this.backgroundMusic.volume = 0.4` sets the volume to 40%
- `this.backgroundMusic.play()` starts playing the audio asynchronously—it doesn't wait for the entire file to load before returning
- `this.setupInputListener()` is called **immediately** after, without waiting for the audio file to fully load or play
- `this.showStartUI()` also executes right away, again without blocking

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

