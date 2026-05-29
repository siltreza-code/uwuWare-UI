# Dont use this, its useless.

## Overview

This is a modular Roblox UI library designed for creating customizable interfaces including windows, toggles, sliders, keybinds, dropdown lists, text inputs, and color pickers.

### It includes:

Window system
Dynamic option system
Global flag storage
Tween-based animations
Drag support
Keybind system
HSV color picker
Dropdown list UI
Slider + textbox syncing

## Installation
```lua
local library = loadstring(game:HttpGet("your-library-url"))()
library:Init()
```

## Creating a Window
```lua
library:CreateWindow(title)
```

Creates a new UI window.

## Parameters
Name	Type	Description
title	string	Window title

## Returns
Window object containing UI element constructors.

## Example
```lua
local window = library:CreateWindow("Main UI")
```

## Flags System

All UI values are stored in:

library.flags
Example
```lua
print(library.flags["AutoFarm"])
library.flags["AutoFarm"] = true
```

Each element automatically syncs its value to a flag if provided.

# UI Elements
## Label
AddLabel(options)

Displays static text.

## Options
Name	Type
text	string
### Example
```lua
window:AddLabel({
    text = "Hello World"
})
```

## Toggle
AddToggle(options)

Creates a boolean switch.

### Options
Name	Type	Default
text	string	required
state	boolean	false
callback	function	nil
flag	string	text

### Example
```lua
window:AddToggle({
    text = "Auto Farm",
    state = false,
    flag = "AutoFarm",
    callback = function(value)
        print("AutoFarm:", value)
    end
})
```

## Button
AddButton(options)

Clickable button.

### Options
Name	Type
text	string
callback	function

## Example
```lua
window:AddButton({
    text = "Click Me",
    callback = function()
        print("Button clicked")
    end
})
```

## Slider
AddSlider(options)

Numeric slider with optional text input.

### Options
Name	Type
text	string
min	number
max	number
value	number
float	number
callback	function
flag	string

### Example
```lua
window:AddSlider({
    text = "Speed",
    min = 0,
    max = 100,
    value = 50,
    float = 1,
    flag = "Speed",
    callback = function(value)
        print(value)
    end
})
```

## Keybind
AddBind(options)

Creates a key or mouse bind.

### Options
Name	Type
text	string
key	Enum.KeyCode / Enum.UserInputType
hold	boolean
callback	function
flag	string

### Example
```lua
window:AddBind({
    text = "Toggle UI",
    key = Enum.KeyCode.RightShift,
    hold = false,
    callback = function()
        library:Close()
    end
})
```

## Dropdown List
AddList(options)

Selectable dropdown menu.

### Options
Name	Type
text	string
values	table
value	string
callback	function
flag	string

### Example
```lua
window:AddList({
    text = "Mode",
    values = {"Easy", "Medium", "Hard"},
    value = "Easy",
    flag = "Mode",
    callback = function(value)
        print(value)
    end
})
```

## Text Box
AddBox(options)

Text input field.

### Options
Name	Type
text	string
value	string
callback	function

### Example
```lua
window:AddBox({
    text = "Username",
    value = "",
    callback = function(text)
        print(text)
    end
})
```

## Color Picker
AddColor(options)

HSV-based color picker with:

Hue slider
Saturation/Value selector
Reset / Undo
Rainbow mode

### Options
Name	Type
text	string
color	Color3
callback	function
flag	string

### Example
```lua
window:AddColor({
    text = "ESP Color",
    color = Color3.fromRGB(255, 0, 0),
    flag = "ESPColor",
    callback = function(color)
        print(color)
    end
})
```

## Folder
AddFolder(title)

Creates a collapsible grouping of UI elements.

### Example
```lua
local folder = window:AddFolder("Combat")

folder:AddToggle({
    text = "Kill Aura",
    flag = "KillAura"
})
```

# Library Functions
## Initialize UI
```lua
library:Init()
```

Renders all windows and UI elements.

## Toggle UI Visibility
```lua
library:Close()
```

Toggles visibility of all windows.

## Instance Helper
```lua
library:Create(class, properties)
```

Creates Roblox instances quickly.

```lua
local frame = library:Create("Frame", {
    Size = UDim2.new(1, 0, 1, 0)
})
```
# Internal Structure
## Flags
library.flags

Stores all UI values globally.

## Windows
library.windows

Stores all created windows.

## Active Popup
library.activePopup

Tracks currently open dropdown/color picker.

# Input Behavior
Windows are draggable via title bar
Only one popup (dropdown/color picker) open at a time
Click outside closes active popup
Keybinds support keyboard and mouse input
Sliders support drag + manual text input
Styling
Dark theme (RGB ~20–40 base)
Smooth tween animations
Rounded UI using sliced ImageLabels
HSV rainbow system
Minimal modern Roblox UI style
