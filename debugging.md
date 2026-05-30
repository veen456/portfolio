---
layout: post 
title: Debugging
hide: true
permalink: /debugging
show_reading_time: false
---

## Console Debugging

What is console debugging?

Console debugging uses `console.log()`, `console.error()` and `console.warn()` print values and track program execution. It's the simplest way to see what your code is doing.

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
    // ... animation frames ...
    hitbox: { widthPercentage: 0.45, heightPercentage: 0.2 }  // 45% width, 20% height
};
```

What does this code do?

- **hitbox object**: Defines the collision detection area for the player sprite
- **widthPercentage: 0.45**: The hitbox is 45% of the sprite's actual width, making it narrower than the visual sprite
- **heightPercentage: 0.2**: The hitbox is only 20% of the sprite's actual height, making it much smaller than the visual sprite
- This configuration creates a small collision box centered on the player, rather than using the entire sprite image
- Benefits: Allows for more forgiving collision detection — the player can get closer to walls/enemies before colliding
- Example: If the sprite is 100px wide × 200px tall, the hitbox would be 45px wide × 40px tall
- The hitbox is typically centered on the sprite for fair collision detection
- During gameplay, this invisible rectangle determines what the player can collide with
- **For debugging**: Visualizing the hitbox shows the actual collision boundary as a colored rectangle overlay on the canvas, helping verify collisions are accurate
- This is more realistic than using the full sprite dimensions, which often includes transparent/empty space

---

## Source-Level Debugging

What is source-level debugging?

Source-level debugging uses browser developer tools to pause code execution at breakpoints, inspect variable values in real-time, and step through code line by line. This is much more powerful than console.log() and lets you see the exact state of your program at any moment.

Benefits of source-level debugging?

- Pause execution at breakpoints
- Step through code line by line (step in, step over, step out)
- Inspect variable values while paused
- View the call stack
- Watch expressions over time
- More powerful than console.log()
- Find bugs faster

```javascript
function updatePlayerPosition(player, direction, speed) {
  // Breakpoint here: debugger; (or click in DevTools)
  
  const moveDistance = speed * 1.5;  // Step through each line
  
  if (direction === 'up') {
    player.y -= moveDistance;
  } else if (direction === 'down') {
    player.y += moveDistance;
  }
  
  // Inspect: player.y should be between 0 and height
  console.log('Player Y:', player.y);
  
  return player;  // Watch what gets returned
}

// Call the function
const player = { x: 100, y: 200, health: 100 };
updatePlayerPosition(player, 'up', 5);
```

How to use source-level debugging:

1. **Open Developer Tools**: Press `F12` or right-click and select "Inspect"
2. **Go to Sources tab**: Click on the "Sources" tab in DevTools
3. **Set a breakpoint**: Click on a line number in your code to pause there
4. **Run your code**: Trigger the function that contains the breakpoint
5. **Code will pause**: Execution stops at the breakpoint
6. **Inspect variables**: Look at the "Variables" or "Scope" section to see current values
7. **Step through code**: Use buttons to move line by line:
   - **Step Over** (F10): Execute next line
   - **Step Into** (F11): Jump into a function call
   - **Step Out** (Shift+F11): Exit current function
8. **Watch expressions**: Add variables to watch panel to see them change
9. **Resume**: Click resume button (or press F8) to continue execution

What does this code do?

- The `debugger;` statement pauses execution if DevTools is open (or manually set a breakpoint by clicking the line number)
- When paused, you can hover over variables to see their values
- Step through `if/else` statements to see which branch executes
- Watch `player.y` change as it moves up (subtracts moveDistance)
- Inspect the final `player` object before it returns
- Compare actual values with expected values to find bugs
- More reliable than guessing with console.log()

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


---

## Application Debugging

What is application debugging?

Application debugging is fixing problems by using the DevTools application tab to look at local storage (ex. cookies, leaderboard, score etc.)

Benefits of application debugging?

- Find and fix application-wide issues
- Understand unexpected behavior
- Improve application reliability
- Track down complex bugs within local storage
- Learn what went wrong

```javascript
// Check if this is first game session, initialize all levels as locked
if (localStorage.getItem('mansionGame_level1_unlocked') === null) {
    // Key does not exist - first time player
    for (let i = 1; i <= 6; i++) {
        localStorage.setItem(`mansionGame_level${i}_unlocked`, 'false');
    }
}
```

What does this code do?

- Checks if `mansionGame_level1_unlocked` exists in localStorage — if null, it's the first time playing
- Creates localStorage keys for all 6 levels, setting each to `'false'` (locked) on first load
- Uses a loop to avoid writing the same code 6 times
- This initializes game progress so the game knows which levels are locked/unlocked

**How to use Application Debugging with this code:**

1. **Open DevTools**: Go to DevTools and go to the "Application" tab
2. **Find Local Storage**: In the left sidebar, click "Local Storage" and select your website
3. **Inspect the keys**: You'll see a table showing all stored key-value pairs:
   - `mansionGame_level1_unlocked: false`
   - `mansionGame_level2_unlocked: false`
   - `mansionGame_level3_unlocked: false` (and so on)
4. **Verify initialization**: Check that all 6 level keys exist and have the correct values
5. **Test unlocking**: Manually change a value by double-clicking it in the table:
   - Change `mansionGame_level2_unlocked` from `false` to `true`
   - Reload the page and see if level 2 is now unlocked in your game
6. **Clear localStorage to test**: Right-click in the LocalStorage table and select "Clear All" to reset, then reload and verify initialization runs again
7. **Debug issues**: If levels aren't unlocking properly, check if the keys are being updated correctly here
8. **Track state changes**: As you play, watch the localStorage values update in real-time to confirm your game is saving progress correctly

This debugging approach helps verify that data is being stored, retrieved, and persisted correctly across game sessions.



---

## Element Inspection

What is element inspection?

Element inspection uses the DevTools element page to let you examine and modify HTML/CSS elements on a web page in real-time using browser developer tools, common bugs include blurry rendering because the height/width of the HTML/CSS is different

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
