---
layout: post 
title: Control Structures
hide: true
permalink: /control-structures
show_reading_time: false
---

## Iteration (Loops)

What is iteration?

Iteration means repeating code multiple times using loops. Instead of writing the same code over and over, you can use a loop to run it as many times as needed using `for`, `while` and `forEach`

Benefits of iteration?

- Repeat actions without duplicating code
- Process all items in an array or list
- Handle repetitive tasks automatically
- Update game objects every frame
- Scale to handle any number of items

# For Loop
```javascript

if (distFromPlayer < minSpawnDist) continue;

                // Check distance from all previously spawned ghosts
    let tooCloseToGhost = false;
        for (const pos of spawnedPositions) {
            const dxGhost = xPos - pos.x;
            const dyGhost = yPos - pos.y;
            const distFromGhost = Math.sqrt(dxGhost * dxGhost + dyGhost * dyGhost);
            if (distFromGhost < minGhostSpacing) {
                tooCloseToGhost = true;
                break;
            }
        }
```

What does this code do?

This code uses a **for loop** to iterate through all previously spawned ghost positions. It:
- Loops through each position stored in `spawnedPositions`
- Calculates the distance from the new ghost position to each existing ghost
- If any ghost is closer than `minGhostSpacing`, it sets the flag `tooCloseToGhost` to true and breaks out of the loop (stops checking)
- This prevents ghosts from spawning too close to each other in the game

# While loop
```javascript
      const edge = Math.floor(Math.random() * 4);
                switch (edge) {
                    case 0: xPos = Math.random() * width;  yPos = -80;          break; // top
                    case 1: xPos = Math.random() * width;  yPos = height + 80;  break; // bottom
                    case 2: xPos = -80;                    yPos = Math.random() * height; break; // left
                    default: xPos = width + 80;            yPos = Math.random() * height; break; // right
                }
```

What does this code do?

This code uses a **switch statement** (often paired with a while loop that keeps trying positions) to:
- Pick a random edge: top (0), bottom (1), left (2), or right (3)
- Set spawn coordinates based on the chosen edge
- Place the object just outside the visible canvas area (at -80 or width/height + 80)
- Use random positioning along the selected edge for variety
- This creates ghost spawning points around the game boundaries

# ForEach loop
```javascript
        const npcs = this.gameEnv.gameObjects.filter(obj => obj.constructor.name === 'Npc');
        npcs.forEach(npc => {
            if (npc && typeof npc.update === 'function') {
                npc.update();
            }
        });
```

What does this code do?

This code uses a **forEach loop** to:
- Filter all game objects to find only the NPCs (non-player characters)
- Loop through each NPC in the filtered array
- Check if the NPC exists and has an `update` function
- Call the `update()` method on each valid NPC
- This allows the game to run update logic for all NPCs every frame (movement, AI, animations, etc.)


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

startWave() {
        if (this.currentWave >= this.waves.length) {
            this.spawnNPC();
            return;
        }

        this.waveActive = true;
        this.waveStartTime = Date.now();
        const wave = this.waves[this.currentWave];

        this.waveEnemies = [];
        this.spawnWaveEnemies(wave.count, wave.speed);
        this.updateWaveDisplay();

        console.log(`Wave ${this.currentWave + 1} started — ${wave.count} enemies at speed ${wave.speed}`);
    }
```

What does this code do?

This code uses an **if statement** to:
- Check if the current wave number has reached the end of the waves array
- If true, spawn an NPC (boss) and return early, skipping the rest of the function
- If false, proceed to initialize and spawn the current wave of enemies
- Set the wave active flag, record the start time, and retrieve wave data
- Spawn the enemies with the specified count and speed, then update the display
- This demonstrates a guard clause pattern: checking for the end condition first and exiting early if needed

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
 if (players.length > 0) {
            const player = players[0];
            const dx = player.position.x - this.position.x;
            const dy = player.position.y - this.position.y;
            const distance = Math.sqrt(dx * dx + dy * dy);

            if (distance > 0) {
                this.position.x += (dx / distance) * this.speed;
                this.position.y += (dy / distance) * this.speed;

                // Flip animation row based on horizontal movement direction
                if (dx > 0 && !this._facingRight) {
                    this._facingRight = true;
                    if (this.spriteData?.right) this.currentAnimation = this.spriteData.right;
                } else if (dx < 0 && this._facingRight) {
                    this._facingRight = false;
                    if (this.spriteData?.left) this.currentAnimation = this.spriteData.left;
                }
            }
        }
```

What does this code do?

This code uses **nested conditionals** to:
- First check if there are any players in the game (outermost condition)
- If true, calculate the distance and direction from the enemy to the player
- Check if the distance is greater than 0 (prevents division by zero)
- If true, move the enemy toward the player using normalized direction vector
- Inside that, check if the enemy is moving right (`dx > 0`) and isn't already facing right
  - If so, update the facing direction and set the appropriate sprite animation
- Otherwise, check if moving left (`dx < 0`) and is currently facing right
  - If so, flip the facing direction and update to the left-facing sprite


