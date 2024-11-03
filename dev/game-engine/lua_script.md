# Stellar Forge : Lua Script

## Overview

Lua scripts are used to define the behavior of game objects. They are attached to game objects as components. The scripts are executed by the game engine at runtime.

## Key Features

- **Scripting Language**: Lua is used as the scripting language for defining game object behavior.
- **Component-based**: Scripts are attached to game objects as components.
- **Runtime Execution**: Scripts are executed by the game engine at runtime.
- **Access to Game Engine**: Scripts can access the game engine API to interact with the game world.

## Example

```lua
-- Define a Lua script for a game object
if start then
    print("Object created!")
    transform.position_x = 100
end
transform.position_x = transform.position_x + 1
```

In this example, the script defines the behavior of a game object. It prints a message when the object is created and then moves the object to the right by incrementing its x position.

## Usage

Create a Lua script file with the desired behavior for a game object. Attach the script to a game object as a component. The script will be executed by the game engine at runtime.
Such as in this json file defining a player object with a LuaScript component:

```json
{
  "id": "d9e329e7-b3bf-412e-86a5-f8e18f710756",
  "meta": {
    "name": "Player"
  },
  "isActive": true,
  "child": [],
  "components": [
    {
      "name": "Transform",
      "data": {
        "invisible": {
          "Position": {
            "x": 0.0,
            "y": 0.0,
            "z": 0.0
          },
          "Rotation": {
            "x": 0.0,
            "y": 0.0,
            "z": 0.0
          },
          "Scale": {
            "x": 1.0,
            "y": 1.0,
            "z": 1.0
          }
        }
      }
    },
    {
      "name": "LuaScriptComponent",
      "data": {
        "invisible": {
          "Script": "assets/objects/scripts/player.lua"
        }
      }
    }
  ]
}

```

In this example, the player object has a LuaScript component that references a Lua script file located at `assets/objects/scripts/player.lua`. The script defines the behavior of the player object.

In a lua script file, you can access:
- `transform` object to manipulate the object's transform.
- `rigidbody` object to manipulate the object's rigidbody.
- `text` object to manipulate the object's text.

There is also a 'start' boolean variable that is true when the object is created and false otherwise.

## Conclusion

Lua scripts are a powerful tool for defining game object behavior in Stellar Forge.
