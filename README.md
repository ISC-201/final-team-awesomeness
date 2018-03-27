# Final - ISC210
Final assignment for ISC210 (2018)
## Game Delivery
- [ ] This assignment will be graded as a Final (30%), it should be built in `Release` mode and targeting `x64` systems.
  - [ ] If you add, or were adding external libraries, check your project settings so everything is bundled properly when changing the build mode and the different architectures.
- [ ] The final build should be uploaded as a zipped file to this repository (copy of the `assignment-10`), only with the binary file and required dependencies for the game to run.

## Source Code Delivery
- [ ] The source code needs to be referenced as a module, accessible from this repository.
- [ ] If you haven't already please create a release for version **v1.0.0**. It should represent your work from *Assignment 7* to *Assignment 10*.
- [ ] This assignment should be final, therefore it should be available as a tagged release as well. Use **v1.0.0**.

## Features
### Levels & Bricks
Breakout contains complete levels with a lot of playfully colored bricks. We want these levels to be flexible such that they can support any number of rows and/or columns. These are the requirements for your `GameLevel` class implementation:

- [ ] Levels have to be stored externally in (text) files. A level should be defined by a single file, and these files should be stored within your **assets** directory in your Game library. Levels can have their own sub-folder.
- [ ] Levels should be defined by a matrix like format, where numbers represent the brick to be rendered. (Brick scale needs to be calculated based on the amount of columns defined in the level matrix and the width of the screen)
  - [ ] Please describe your level file structure on the README file of your source repository.
- [ ] Levels should add solid bricks (that cannot be destroyed)
- [ ] Levels have to support multiple brick colors. Sprites are in grey scale, therefore fragment arithmetic should help to achieve this from a single brick texture.
- [ ] Levels should be rendered from top to bottom. The top-most row of your level matrix should be at the border of the top of the screen.
- [ ] Levels should be loaded by your `Scene` object.
- [ ] You should at least have `3` levels.

### The Paddle
In Breakout, the player controls a paddle to bounce a ball of up and down in order to destroy the level bricks. These are the requirements for your `Paddle` class implementation:

- [ ] The paddle should be rendered at the bottom of the screen. You should use the provided paddle texture.
- [ ] The paddle only allows for horizontal movement and whenever it touches any of the screen's edges, its movement should halt.
  - [ ] The paddle should only be moved when pressing the left and right arrow keys or the **A** and **D** keys.
- [ ] The paddle `GameObject` should be defined by a position, size and a texture.

### The Ball
In Breakout, the ball has two states, it's either stuck on the player paddle or in free movement. When the game starts, the ball is initially stuck on the player paddle until the player starts the game by pressing some arbitrary key. These are the requirements for your `Ball` class implementation:

- [ ] The ball should be stuck in the paddle at the beginning of the game.
- [ ] The ball should be released from the paddle when pressing the **SPACE** key.
- [ ] At this point, the ball should bounce around the screen's vertical edges and top horizontal edges (window bounds).
  - [ ] You can achieve this by reversing the ball's velocity and restoring its position to a valid one. You can also read about vector reflection.
  - [ ] The ball can "fall through" the bottom horizontal edge of the screen.

### Collision detection
When trying to determine if a collision occurs between two objects, we generally do not use the data of the objects themselves since these objects are often quite complicated; this in turn also makes the collision detection complicated. A common practice is to represent `GameObjects` as primitive shapes and using simple arithmetic to determine intersections between these shapes. In our previous game we used circle-to-circle collision detection. In this one, we will use Circle-to-AABB collision detection.

**AABB** stands for axis-aligned bounding box which is a rectangular collision shape aligned to the base axes of the scene, which in 2D aligns to the x and y axis. Being axis-aligned means the rectangular box is not rotated and its edges are parallel to the base axes of the scene (e.g. left and right edge are parallel to the y axis). The fact that these boxes are always aligned to the axes of the scene makes all calculations easier. AABB's are ideal to represent our bricks.

In order to achieve collision detection you need to create a new component. These are the requirements for it:
- [ ] Let's call your component a `CollisionComponent`.
- [ ] The `CollisionComponent` should be attached to `GameObjects` that handle collision, these are: the ball, the bricks and the paddle.
- [ ] The primitive representing the game object bounding box should be configured when creating the component. The paddle and bricks should use an *AABB* and the ball should use a *Circle*.
- [ ] Add a mechanism to handle intersection testing between any of the primitive shapes representing the components. Since the ball is the only moving object on the screen the test will be mostly Circle-to-AABB.
- [ ] Your component should handle the state of the object, and should have an accessor that exposes if the object is colliding with another object or not.
- [ ] Your game implementation should remove the colliding bricks that are **NOT SOLID** once the are hit by the ball.

### Collision resolution
The ball needs to react to the collisions e.g. update its position and/or velocity whenever a collision occurs. These are the requirements to achieve this:

-[ ] Change the ball's velocity if:
  * If the ball collides with the right or left side of an AABB, its horizontal velocity (x) is reversed.
  * If the ball collides with the bottom or top side of an AABB, its vertical velocity (y) is reversed. 

Collisions between the ball and the player are slightly different since this time the ball's horizontal velocity should be updated based on how far it hits the paddle from its center. The further the ball hits the paddle from its center, the stronger its horizontal velocity should be.

### Font rendering & Score
- [ ] Players should score points for destroying bricks. You should come up with your own criteria for the score value per destroyed brick.
- [ ] Players should have 3 lives, and earn an extra life every `X` amount of points. Lives should be represented as balls and should be drawn on the top right corner of the screen. Take into account rendering adjustments for lives added or removed.
- [ ] The score should be drawn in the top left corner of the screen.

### Sounds
- [ ] Feel free to add the sounds effects you see fit, but add at least one.

### Game mechanics
- [ ] Level transitions should occur right when the level is out of destroyable bricks. How these happen is totally up to you. You can start right away a new level or you can have a cool down phase and restart everything from scratch.
- [ ] A player looses a life every time the ball passes the bottom of the screen. A player looses the game when it runs out of lives.
- [ ] Feel free to add power ups and interesting game mechanics that complement the game experience without compromising the original requirements.
- [ ] Display a "Game Over" message once the player runs out of lives.
- [ ] Display a "You Win!" message and the total score once a player completes all of the levels of your game.
- [ ] Add debug tools as you see fit. These are not mandatory but might be useful to achieve the final goal of this project.

## Grading
Since this is a final evaluation will be different. The overall grade will be 30% of the total grade for the class. The distribution of this grade will be as follows:

* 50% of the grade will be attributed using the grading Rubric attached to this repository.
* 50% of the grade will be attributed using the following "GAMING EXPERIENCE" criteria:
  * 30% End-user game experience. This defines how good the game feels or how close is the experience to the real game.
  * 30% Text rendering
  * 30% Sound support
  * 10% Re-spawing, game over and re-starting the game
	
## Extra credit
- [ ] Add shader post-processing effects.
- [ ] Add power ups, like a sticky paddle or a longer paddle.
- [ ] Auto-generate the game levels. (Never ending game).
- [ ] Add game modes and other experience compliments that you think would make for a better gaming experience.

Attribution of the extra credit will only happen if all of the "GAMING EXPERIENCE" requirements are met. 