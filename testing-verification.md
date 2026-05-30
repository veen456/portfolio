---
layout: post 
title: Testing & Verification
hide: true
permalink: /testing-verification
show_reading_time: false
---

## Gameplay Testing

What is gameplay testing?

Gameplay testing is manually playing through your game to verify all features work correctly, game mechanics function as intended, and the player experience is smooth and fun.

Benefits of gameplay testing?

- Find bugs that automated tests miss
- Verify game feels fun and balanced
- Test user experience and controls
- Catch gameplay edge cases
- Ensure game is playable

Here is a link to a working mansion game: [Mansion Game](https://jas-bop.github.io/pages/gamify/mansionGame)


---

## Integration Testing

What is integration testing?

Integration testing verifies that different parts of your game work together correctly. It tests how systems interact, like how the UI, game logic, and rendering all work as one.

Benefits of integration testing?

- Verify systems work together
- Test game state management
- Check UI updates correctly
- Ensure data flows between modules
- Catch interaction bugs

```javascript
// Example: Testing level progression system
class LevelManager {
    constructor() {
        this.currentLevel = 1;
        this.levelScores = {};
        this.allLevelsCompleted = false;
    }

    completeLevel(score) {
        // Store score for current level
        this.levelScores[this.currentLevel] = score;
        
        // Check if all levels are complete
        if (this.currentLevel === 6) {
            this.allLevelsCompleted = true;
            console.log("Game completed!");
        } else {
            // Progress to next level
            this.currentLevel += 1;
        }
        
        // Update UI
        this.updateLevelDisplay();
        return this.allLevelsCompleted;
    }

    updateLevelDisplay() {
        const display = document.getElementById('levelDisplay');
        if (display) {
            display.textContent = `Level ${this.currentLevel}`;
        }
    }

    getTotalScore() {
        return Object.values(this.levelScores).reduce((sum, score) => sum + score, 0);
    }
}
```

What does this code do?

- Manages game progression through multiple levels (1-6)
- Stores score for each completed level
- Automatically advances to next level or marks game as completed
- Updates the UI to show current level
- Calculates total score across all levels
- **Testing this:** Complete a level and verify: score saves, level number increments, UI updates, and level 6 triggers game completion

---

## API Error Handling

What is API error handling?

API error handling catches and manages errors that occur when communicating with servers. It ensures the game doesn't crash and provides user-friendly error messages when things go wrong.

Benefits of API error handling?

- Prevent crashes from network errors
- Provide user feedback on failures
- Log errors for debugging
- Allow graceful degradation
- Improve user experience

```javascript
// Example: Handling API errors when loading game data
async function loadPlayerProgress(playerId) {
    try {
        // Attempt to fetch player data from server
        const response = await fetch(`/api/players/${playerId}/progress`);
        
        // Check if response was successful
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        // Parse and return the data
        const playerData = await response.json();
        console.log("Player data loaded:", playerData);
        return playerData;
        
    } catch (error) {
        // Handle network errors or parsing errors
        console.error("Failed to load player progress:", error);
        
        // Show error message to player
        const errorDisplay = document.getElementById('errorMessage');
        if (errorDisplay) {
            errorDisplay.textContent = "Could not load your progress. Please try again.";
        }
        
        // Return default data to allow game to continue
        return { level: 1, score: 0, health: 100 };
    }
}

// Usage
const playerData = await loadPlayerProgress(123);
console.log("Loaded data or defaults:", playerData);
```

What does this code do?

- **try block**: Attempts to fetch player progress from the server
- **response.ok check**: Verifies the server responded with success (status 200-299)
- **throw Error**: Creates an error if response failed
- **response.json()**: Parses JSON response data
- **catch block**: Catches any network errors, parsing errors, or thrown errors
- **Error logging**: Logs the error for debugging purposes
- **User feedback**: Displays a user-friendly error message on the page
- **Graceful fallback**: Returns default data so the game can continue even if the server is down
- **Testing this:** Simulate network failure by disabling WiFi or using DevTools Network tab to block the API call, then verify error message displays and game continues with defaults

---

