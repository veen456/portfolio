---
layout: post 
title: Object Oriented Programming
hide: true
permalink: /OOP
show_reading_time: false
---

## Writing Classes

What is writing classes?

Writing classes are a big part of OOP (Object Oriented Programming). A class is an organized, repeatable way to make multiple functions for an object that share similar properties.

Benefits of writing classes?

- Code reusability - write once, use many times
- Efficiency - multiple functions in one class
- Organization - organize related properties and methods together
- Scalability - easy to manage multiple objects
- Maintainability - changes in one place affect all instances

```javascript
// Example class defining a game level with characters
class GameLevelPatrollingGuard {
    constructor(data) {
        this.level = data.level || 1;
        this.background = new Background(data.bg);
        this.player = new Player(data.player);
        this.npc = new PatrollingGuard(data.npc);
        this.gameObjects = [this.background, this.player, this.npc];
    }
    
    configureGameArea(canvas, ctx) {
        // Render all game objects
        this.gameObjects.forEach(obj => obj.draw(ctx));
    }
}

// Usage
const levelData = { level: 1, bg: {...}, player: {...}, npc: {...} };
const gameLevel = new GameLevelPatrollingGuard(levelData);
```

What does this code do?

- Defines a `GameLevelPatrollingGuard` class with a constructor
- Constructor accepts data and creates game objects
- Stores background, player, and NPC in `gameObjects` array
- `configureGameArea()` method renders all game objects
- Shows how a single class organizes multiple related functions
- Demonstrates constructor patterns and instance creation

```javascript
// Child class extending parent class
class ExampleEnemy extends Enemy {
    constructor(data, gameEnv) {
        super(data, gameEnv);
        this.enemyType = 'Example';
    }
    
    handleCollisionEvent(projectile) {
        // Override: detect collision with player
        if (this.collidesWith(projectile)) {
            console.log("Enemy hit! Destroying player...");
            projectile.destroy();
        }
    }
}
```

What does this code do?

- Extends `Enemy` parent class to create child class
- Calls `super()` to initialize parent properties
- Adds `enemyType` property specific to this enemy
- Overrides `handleCollisionEvent()` method
- Shows collision detection and object destruction
- Demonstrates inheritance and method overriding together

---

## Methods & Parameters

What are methods and parameters?

Methods are reusable blocks of code that perform specific tasks. Parameters are inputs to methods that let you pass data and customize behavior.

Benefits of methods and parameters?

- Reusability - write code once, call many times
- Flexibility - customize behavior through parameters
- Maintainability - easier to update and debug
- Clarity - descriptive names make code readable
- Organization - group related functionality

```javascript
// Class with multiple methods and parameters
class Guard {
    constructor(data, gameEnv) {
        this.x = data.x;
        this.y = data.y;
        this.health = 50;
        this.vx = 2;
        this.vy = 0;
    }
    
    // Method with parameters
    update(canvas) {
        this.stayWithinCanvas(canvas);
    }
    
    // Method to keep guard within canvas boundaries
    stayWithinCanvas(canvas) {
        if (this.x < 0 || this.x + 50 > canvas.width) {
            this.vx *= -1;
        }
        this.x += this.vx;
    }
    
    // Collision detection method
    handleCollisionEvent(projectile) {
        if (this.collidesWith(projectile)) {
            console.log("Guard hit!");
            projectile.destroy();
        }
    }
}
```

What does this code do?

- Constructor takes `data` and `gameEnv` parameters to customize each instance
- `update()` method takes canvas parameter for boundary checking
- `stayWithinCanvas()` keeps guard bouncing within bounds
- `handleCollisionEvent()` detects collisions with projectiles
- Shows methods with different parameters and purposes
- Demonstrates how parameters customize behavior

---

## Instantiation & Objects

What is instantiation?

Instantiation means creating a new instance (copy) of an object from a class blueprint. Each instance has its own properties and data.

Benefits of instantiation?

- Create multiple objects from one template
- Reusability - same class for many objects
- Organization - cleaner code structure
- Easy management - change instances independently
- Scalability - quickly add more objects

```javascript
// Define configuration objects
const bgData = {
    path: "/images/gamebuilder/backgrounds/",
    width: 800,
    height: 600
};

const playerData = {
    x: 100,
    y: 300,
    width: 50,
    height: 50
};

const npcData = {
    x: 200,
    y: 300,
    width: 50,
    height: 50,
    speed: 2
};

// Instantiate objects from classes
const background = new GameEnvBackground(bgData);
const player = new Player(playerData);
const npc = new ExampleEnemy(npcData);

console.log("Player position:", player.x, player.y);
console.log("NPC position:", npc.x, npc.y);
```

What does this code do?

- Creates data objects with configuration properties
- Uses `new` keyword to instantiate classes
- Each `new` call creates separate instance with own properties
- Can access and modify properties independently
- Shows how configuration data becomes class instances
- Demonstrates three separate objects from different classes

---

## Inheritence

What is inheritance?

Inheritance allows classes to acquire properties and methods from parent classes. Child classes can reuse parent code and add their own specialized behavior.

Benefits of inheritance?

- Reuse code - write once in parent, use in all children
- Create specialized versions - customize child behavior
- Reduce duplication - avoid repeating code
- Organize hierarchies - create logical class relationships
- Share functionality - common methods in one place

```javascript
// Parent class with common properties and methods
class Character {
    constructor(name, health) {
        this.name = name;
        this.health = health;
        this.isDead = false;
    }
    
    takeDamage(damage) {
        this.health -= damage;
        if (this.health <= 0) {
            this.isDead = true;
            console.log(this.name + " is dead!");
        }
    }
}

// Child class extends parent
class Guard extends Character {
    constructor(name, health) {
        super(name, health);
        this.patrolRadius = 100;
    }
    
    patrol() {
        console.log(this.name + " is patrolling...");
    }
}

// Usage
const guard = new Guard("Guard1", 50);
guard.takeDamage(10); // Uses parent method
guard.patrol(); // Uses child method
```

What does this code do?

- `Character` parent class defines common properties (name, health)
- `takeDamage()` is shared by all children
- `Guard` child class calls `super()` to initialize parent
- Guard adds specialized property `patrolRadius`
- Guard adds specialized method `patrol()`
- Shows how child reuses parent code while adding own features

```javascript
// Another inheritance example
class Entity {
    constructor(x, y) {
        this.x = x;
        this.y = y;
        this.vx = 0;
        this.vy = 0;
    }
    
    move() {
        this.x += this.vx;
        this.y += this.vy;
    }
}

// Player adds score tracking to Entity
class Player extends Entity {
    constructor(x, y) {
        super(x, y);
        this.score = 0;
    }
    
    addScore(points) {
        this.score += points;
    }
}

// Usage
const player = new Player(100, 300);
player.move(); // From parent
player.addScore(10); // From child
```

What does this code do?

- `Entity` parent class provides position and movement
- `Player` child class calls `super(x, y)` for position
- Player adds score-tracking functionality
- Child inherits `move()` from parent
- Child adds `addScore()` method
- Shows inheritance creating specialized versions of common class

---

## Method Overriding

What is method overriding?

Method overriding means creating a new version of a parent class's method in a child class. Instead of using the parent's method, the child uses its own customized version.

Benefits of method overriding?

- Customization - each child class behaves differently
- Polymorphism - call method on any child, correct behavior runs
- Flexibility - change behavior without changing parent
- Code reuse with differences - keep common code, change specifics
- Cleaner code - no need for conditional logic

```javascript
// Parent class with methods
class Enemy {
    constructor(data, gameEnv) {
        this.x = data.x;
        this.y = data.y;
        this.health = 100;
        this.vx = 2;
    }
    
    handleCollisionEvent(projectile) {
        console.log("Generic enemy hit");
    }
    
    stayWithinCanvas(canvas) {
        if (this.x < 0 || this.x + 50 > canvas.width) {
            this.vx *= -1;
        }
    }
}

// Guard child overrides both methods
class Guard extends Enemy {
    handleCollisionEvent(projectile) {
        // Override: destroy player instead
        console.log("Guard hit! Destroying player...");
        projectile.destroy();
        this.health -= 10;
    }
    
    stayWithinCanvas(canvas) {
        // Override: bounce at edges
        if (this.x < 0 || this.x + 50 > canvas.width) {
            this.vx *= -1;
            this.x += this.vx;
        }
    }
}

// ExampleEnemy overrides only collision
class ExampleEnemy extends Enemy {
    handleCollisionEvent(projectile) {
        // Override collision behavior
        console.log("Example enemy explodes!");
        projectile.destroy();
    }
    
    // Keeps parent stayWithinCanvas
}
```

What does this code do?

- Parent `Enemy` class defines default methods
- `Guard` child overrides both `handleCollisionEvent()` and `stayWithinCanvas()`
- `ExampleEnemy` child only overrides `handleCollisionEvent()`
- Each child can have completely different behavior
- Shows flexibility of method overriding
- Demonstrates partial override - some methods from parent, some custom

---

## Constructor Chaining

What is constructor chaining?

Constructor chaining means one constructor calls another constructor so you can reuse setup code. This happens in classes with `extends` and `super()`.

Benefits of constructor chaining?

- Avoid repeating initialization code
- Parent code runs first, then child code
- Clean initialization of inheritance hierarchies
- Automatic parent property setup
- Maintainable inheritance relationships

```javascript
// Parent class with constructor
class Enemy {
    constructor(data, gameEnv) {
        this.name = data.name;
        this.x = data.x;
        this.y = data.y;
        this.health = data.health || 50;
        this.vx = 0;
        this.vy = 0;
        console.log(this.name + " created");
    }
}

// Child class calls parent constructor with super()
class Guard extends Enemy {
    constructor(data, gameEnv) {
        super(data, gameEnv); // Calls parent constructor first
        
        // Child-specific initialization
        this.velocity = 2;
        this.patrolRadius = 100;
        console.log(this.name + " is guarding with velocity " + this.velocity);
    }
}

// Usage
const guardData = { name: "Guard1", x: 100, y: 300, health: 75 };
const guard = new Guard(guardData, gameEnv);
```

What does this code do?

- `super(data, gameEnv)` calls parent constructor first
- Parent constructor initializes name, x, y, health, velocities
- After parent setup complete, child code runs
- Child adds Guard-specific properties (velocity, patrolRadius)
- Console shows parent initialization first, then child
- Demonstrates proper constructor chaining pattern

```javascript
// More complex constructor chaining
class Enemy {
    constructor(name, health) {
        this.name = name;
        this.health = health;
        console.log("Enemy: " + name + " initialized");
    }
}

class Guard extends Enemy {
    constructor(name, health, patrolArea) {
        super(name, health);
        this.patrolArea = patrolArea;
        console.log("Guard: patrol area set");
    }
    
    stayWithinCanvas(canvas) {
        // Override with bounce behavior
        if (this.x < 0 || this.x + 50 > canvas.width) {
            this.vx *= -1;
        }
    }
}

class EliteGuard extends Guard {
    constructor(name, health, patrolArea, armor) {
        super(name, health, patrolArea);
        this.armor = armor;
        console.log("EliteGuard: armor equipped");
    }
}

// Usage shows multi-level chaining
const elite = new EliteGuard("Elite1", 150, 200, 50);
// Console output:
// Enemy: Elite1 initialized
// Guard: patrol area set
// EliteGuard: armor equipped
```

What does this code do?

- Shows multi-level inheritance (EliteGuard → Guard → Enemy)
- `super()` in Guard calls Enemy constructor
- `super()` in EliteGuard calls Guard constructor
- Constructor chaining propagates up the hierarchy
- Each level initializes its own properties
- Shows proper execution order in inheritance chain

