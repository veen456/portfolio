---
layout: post 
title: Documentation
hide: true
permalink: /documentation
show_reading_time: false
---

## Code Comments

What are code comments?

Code comments are notes you add to your code that the computer ignores. They help explain what your code does so others (and future you) can understand it.

- Uses `//` for single line comments
- Uses `/* */` for multi-line comments
- Computer ignores all comments
- Comments explain what code does
- Shows proper commenting practice

Benefits of code comments?

- Explain complex code logic
- Document why decisions were made
- Help team members understand code
- Make code easier to maintain
- Leave notes for debugging

```javascript
// Import required game engine classes
import GameEnvBackground from '@assets/js/GameEnginev1/essentials/GameEnvBackground.js';
import Player from '@assets/js/GameEnginev1/essentials/Player.js';
import Npc from '@assets/js/GameEnginev1/essentials/Npc.js';
import ExampleEnemy from '@assets/js/projects/collisions-mechanic/levels/ExampleEnemy.js';

// Define the game level class
class GameLevelCollisionMechanicsLessonLevel {
    constructor(gameEnv) {
        // Get game environment properties
        const path = gameEnv.path;
        const width = gameEnv.innerWidth;
        const height = gameEnv.innerHeight;

        // Configure background sprite
        const bgData = {
            name: "custom_bg",
            src: path + "/images/gamebuilder/bg/alien_planet.jpg",
            pixels: { height: 772, width: 1134 }
        };

        // Configure player sprite and animations
        const playerData = {
            id: 'playerData',
            src: path + "/images/gamebuilder/sprites/astro.png",
            SCALE_FACTOR: 5,
            STEP_FACTOR: 1000,
            ANIMATION_RATE: 50,
            // Starting position
            INIT_POSITION: { x: 100, y: 300 },
            pixels: { height: 770, width: 513 },
            // Sprite sheet organization
            orientation: { rows: 4, columns: 4 },
            // Animation frames for each direction
            down: { row: 0, start: 0, columns: 3 },
            downRight: { row: 1, start: 0, columns: 3, rotate: Math.PI/16 },
            downLeft: { row: 0, start: 0, columns: 3, rotate: -Math.PI/16 },
            left: { row: 2, start: 0, columns: 3 },
            right: { row: 1, start: 0, columns: 3 },
            up: { row: 3, start: 0, columns: 3 },
            upLeft: { row: 2, start: 0, columns: 3, rotate: Math.PI/16 },
            upRight: { row: 3, start: 0, columns: 3, rotate: -Math.PI/16 },
            // Hitbox for collision detection
            hitbox: { widthPercentage: 0, heightPercentage: 0 },
            // Keyboard controls (WASD keys)
            keypress: { up: 87, left: 65, down: 83, right: 68 }
            };

        // Configure enemy/NPC sprite
        const npcData = {
            id: 'ufo',
            greeting: 'Hello!',
            src: path + "/images/gamebuilder/sprites/ufos.png",
            SCALE_FACTOR: 8,
            ANIMATION_RATE: 50,
            // Starting position
            INIT_POSITION: { x: 259, y: 223 },
            pixels: { height: 500, width: 500 },
            // Sprite sheet organization
            orientation: { rows: 4, columns: 3 },
            // Animation frames for each direction
            down: { row: 0, start: 0, columns: 3 },
            right: { row: Math.min(1, 4 - 1), start: 0, columns: 3 },
            left: { row: Math.min(2, 4 - 1), start: 0, columns: 3 },
            up: { row: Math.min(3, 4 - 1), start: 0, columns: 3 },
            upRight: { row: Math.min(3, 4 - 1), start: 0, columns: 3 },
            downRight: { row: Math.min(1, 4 - 1), start: 0, columns: 3 },
            upLeft: { row: Math.min(2, 4 - 1), start: 0, columns: 3 },
            downLeft: { row: 0, start: 0, columns: 3 },
            // Hitbox for collision detection
            hitbox: { widthPercentage: 0.1, heightPercentage: 0.2 },
        };

        // Register all game objects for this level
        this.classes = [      
            { class: GameEnvBackground, data: bgData },
            { class: Player, data: playerData },
            { class: ExampleEnemy, data: npcData }
        ];
    }
}

// Export the level configuration
export default GameLevelCollisionMechanicsLessonLevel;
```

---

## Mini-Lesson Documentation

What is documentation?

Documentation is written explanation of how code works, including parameters, return values, and usage examples. Good documentation makes code easier to use.

Benefits of documentation?

- Explain how to use functions
- Document parameters and return values
- Provide usage examples
- Help other developers
- Make code self-explanatory

### Goal

Teach the class what collision mechanics are, how to use them, and how to successfully implement them into their own game.

### Files Added 

- `_projects/games/collisions-mechanic/notebook.src.ipynb`
- `_projects/games/collisions-mechanic/levels/ExampleEnemy.js`
- `_projects/games/collisions-mechanic/levels/GameLevelCollisionMechanicsLessonLevel.js`
- `_projects/games/collisions-mechanic/levels/GameLevelPatrollingGuard.js`
- `_projects/games/collisions-mechanic/levels/ GameLevelPatrollingGuardBroken.js`
- `_projects/games/collisions-mechanic/levels/Guard.js`
- `_projects/games/collisions-mechanic/levels/GuardBroken.js` 
- `_projects/games/collisions-mechanic/images/alien_planet.jpg`
- `_projects/games/collisions-mechanic/images/astro.png`
- `_projects/games/collisions-mechanic/images/ufos.png`

### What We Implemented

We implemented couple game runner cells to demonstrate how collision mechanics work and how to add it into someone's game. We didn't just explain what they are, we showed how to add applications of them, for example adding guards that can kill the player.

### How We Tested

- Ran `make dev`
- Used localhost to confirm our changes were what we wanted before pushing to github.
- Checked that the gamerunner cells worked in localhost and deployed.
- Made sure the sample games had application of collision mechanics (guards, ground, etc.)
- Confirmed that the collision mechanics in the gamerunner was correctly implemented and worked fine.

### What We Learned

- A level is easier to maintain and control when all of the files are in the same project
- Taking your time to document all of your progress slowly over time helps show your progress and document all the small decisions made along the way to get to the final result
- Documentation is a part of the building process, not extra work.

### Next Step

Helping other groups implement collision mechanics and adding better implementations of it in our own game.

---

## Code Highlights

What are code highlights?

Code highlights use color and formatting to make different parts of code visually distinct, improving readability and understanding.

Benefits of code highlights?

- Identify different code elements quickly
- Spot syntax errors visually
- Make code easier to read
- Distinguish keywords from variables
- Improve code understanding

```javascript
// Keywords are highlighted
const player = { name: 'Astro', health: 100 };
let position = 0;

// Function keywords highlighted
function movePlayer(x, y) {
    // Comments are typically green
    player.x = x;
    player.y = y;
    // Strings are shown in quotes
    console.log("Player moved");
}

// Numbers highlighted differently
const distance = 100;
const multiplier = 2.5;

// Booleans highlighted
const isAlive = true;
const canMove = player.health > 0;
```

What does this code do?

- Keywords like `const`, `let`, `function` are highlighted differently
- Comments appear in one color (usually green)
- Strings in quotes appear in another color
- Numbers highlighted separately from identifiers
- Boolean values like `true` and `false` highlighted
- Syntax highlighting helps catch errors quickly
