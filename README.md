# 2D Game Engine
 
A component-based 2D game engine built in C++ using SDL2 and ImGui. Designed and built as a final project, the engine features a fully functional scene editor and a separate play mode runtime, allowing users to design and play simple 2D platformer games without writing any code.

---
 
## Screenshot
 
*Screenshot here*
 
---
 
## Features
 
- **Scene Editor** — place, move, resize, recolor, and name entities directly in the viewport
- **Hierarchy Panel** — lists all entities in the scene, select or remove them with a click
- **Inspector Panel** — edit every property of the selected entity including shape, size, color, position, and behavior flags
- **Shape Support** — Rectangle, Square, and Circle
- **Play / Stop** — hit Play to run the game, Stop to return to the editor with the scene fully intact
- **Player Movement** — assign player movement to any entity of your choice
- **Gravity & Jumping** — the player entity falls under gravity and can jump with W or Space
- **AABB Collision** — solid entities act as platforms the player can land and stand on
- **Goal System** — mark any entity as the Goal; touching it ends the game
- **Color Picker** — full RGB color control per entity
---
 
## Built With
 
- **C++17**
- **SDL2** — window creation, rendering, input handling, and the game loop
- **ImGui** — immediate mode GUI for all editor panels, running on top of SDL2
---
 
## Project Structure
 
```
src/
  core/
    Entity.hpp          - Game object container, stores and ticks components
    Component.hpp       - Base class for all behaviors
  engine/
    Engine.hpp          - Editor class, manages the scene and UI
    Engine.cpp          - Main loop, event handling, rendering, collision detection
  components/
    Transform.hpp       - Stores x and y position for any entity in the world
    PlayerMovement.hpp  - Reads keyboard input and applies velocity each frame
  runtime/
    Runtime.hpp         - Play mode class, runs the simulation independently
    Runtime.cpp         - Gravity, input, AABB collision resolution, goal detection
    SceneData.hpp       - Plain data structs, the bridge between editor and runtime
```
 
---
 
## Architecture
 
The engine is split into two completely separate systems:
 
**Editor** (`Engine`) manages the scene in design time. Entities are placed, sized, and configured here. No physics or simulation runs in editor mode.
 
**Runtime** (`Runtime`) takes a snapshot of the scene via `SceneData` when Play is hit and runs the simulation independently. The editor scene is never modified during play — when Stop is hit the runtime is destroyed and the scene is exactly as it was left.
 
### Entity Component System
 
Entities are containers of components. Rather than using deep inheritance hierarchies, behavior is added by composing components onto any entity. The `Component` base class uses polymorphism so the engine calls `Update(deltaTime)` on every component each frame through a base class pointer.
 
### Collision Detection
 
AABB (Axis-Aligned Bounding Box) collision is used for platform detection and goal triggering. The runtime checks the player's bounding box against all solid entities each frame and resolves overlaps by finding the smallest overlap axis and pushing the player out in that direction.
 
---
 
## How to Build
 
**Requirements:**
- CMake 3.28+
- SDL2
- C++17 compiler
```bash
mkdir build
cd build
cmake ..
make
./GameEngine
```
 
---
 
## How to Use
 
1. **Add Entity** — click Add Entity in the Hierarchy panel
2. **Place Entity** — click anywhere in the viewport to place the selected entity
3. **Configure** — use the Inspector to set shape, size, color, and behavior
4. **Mark Solid** — check Solid on any entity you want to act as a platform
5. **Mark Goal** — check Goal on the entity the player needs to reach
6. **Add Player Movement** — check Player Movement on the entity the player will control
7. **Play** — hit Play in the menu bar to run the game
8. **Stop** — hit Stop to return to the editor
---
 
## Controls (Play Mode)
 
| Key | Action |
|-----|--------|
| A | Move Left |
| D | Move Right |
| W / Space | Jump |
| Escape | Quit |
 
---

Author
Evan Castner — Interactive Game Design, Spring 2026
