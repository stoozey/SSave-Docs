# Getting Started

## Introduction

The purpose of this tool is to provide a simple way to manage saves and user settings in your project. Once you understand the basics, you can very easily integrate it into your games.

## Installation

Download the latest release from [GitHub](https://github.com/stoozey/SSave/releases) or [Itch.io](https://stoozey.itch.io/ssave).
In GameMaker, go to `Tools > Import Local Package` and select the downloaded `.yymps` file.

You'll see two folders: `SSave` and `Demo`. The demo includes a demonstration of the SSave system in use, if you aren't going to try it out, you only need to import the `SSave` folder.

## Setting Up a SaveFile Class

Create a new script and inside it, add this code:

```js
function SaveFile() : SSave("save") {
    add_value("points", SSAVE_TYPE.REAL, 0);
}
```

This creates a new save file class that contains a `points` value. The `"save"` argument in the `SSave("save")` constructor is the name of the file that gets saved to disk. For example, this will save to `save.ssave`. You can leave out this argument, in which case it will default to `data.ssave`.

When creating save classes, you need to extend the `SSave` class. This is so you can call the [`add_value()`](ssave.md#ssaveadd_valuename-type-default) method within it's constructor.

## Working With the SaveFile Class

### Setup

Before we start, create a new object and add this code to it:

```js title="Create Event"
points = 0;

// we will define these functions later
Save = function() { };
Load = function() { };

Load();
```

```js title="Step Event"
if (keyboard_check_pressed(vk_space)) {
    points += 1;
}

if (mouse_check_button_pressed(mb_left)) {
    Save();
}

if (mouse_check_button_pressed(mb_right)) {
    Load();
}
```

```js title="Draw Event"
draw_text(0, 0, $"Points: {points}");
```

Now that we have this basic object set up, we can begin implementing the `Save` and `Load` functions.

### Saving and Loading

When accessing save files, you have two options: manually creating save instances or allowing the [`SSaveManager`](ssave-manager.md) to handle it for you.

Here I will cover how to use the manager, as it greatly simplifies the process of managing your saves. If you want to see an example of how to manage saves manually, check out [this example](examples.md#using-ssave-without-the-manager).

```js title="Create Event"
Save = function() {
    var _save = ssave_get(SaveFile);
    _save.set("points", points);
    _save.save();
}

Load = function() {
    var _save = ssave_get(SaveFile);
    points = _save.get("points");
}
```

The bread-and-butter of this code is the [`ssave_get()`](ssave-manager.md#ssave_getssaveconstructor-fileprefix) function, which retrieves a persistent instance of the `SaveFile` class. If it has not yet been loaded, it will automatically do so. If there is no file on disk to load, the class will just have the default values.

Once you've called [`ssave_get()`](ssave-manager.md#ssave_getssaveconstructor-fileprefix) for the first time, the save class will be stored inside of the manager. Subsequent calls to [`ssave_get()`](ssave-manager.md#ssave_getssaveconstructor-fileprefix) will return this same instance, allowing you efficiently access and modify the save data from anywhere in your code without needing to load the file each time.

### Multiple Saves

What if we want to have multiple save slots? This is where the `filePrefix` argument comes in.

Right now, our save file is reading and writing to `save.ssave`. If we set the `filePrefix` to `1`, it would read and write to `1save.ssave`.

***Note: you can use any string or number as a prefix.***

With this knowledge, we can modify our `Save` and `Load` functions to treat the `filePrefix` as a slot index:

```js title="Create Event"
slotIndex = 0;

Save = function() {
    var _save = ssave_get(SaveFile, slotIndex);
    _save.set("points", points);
    _save.save();
}

Load = function() {
    var _save = ssave_get(SaveFile, slotIndex);
    points = _save.get("points");
}

SetSlotIndex = function(_slotIndex) {
    Save(); // save the current slot before changing
    slotIndex = _slotIndex;
    Load(); // load the new slot
}

Load();
```

And in our step event let's listen for keys 0-9 to change the slot index:

```js title="Step Event"
for (var i = 0; i < 10; i++) {
    if (keyboard_check_pressed(ord(string(i)))) {
        SetSlotIndex(i);
        break;
    }
}

// rest of the code remains the same
```

### Chaining Functions

SSave functions can be chained together for convenience. We could update the `Save` function to look like this:

```js title="Create Event"
Save = function() {
    ssave_get(SaveFile, slotIndex)
        .set("points", points)
        .save();
}
```

If you're unsure which functions can be chained, take a look at the return type of functions in the [`SSave`](ssave.md) section.

## Conclusion

You should now be able to save via the left mouse button and load via the right mouse button. The points should increase when you press space. You can save to 10 different slots, and if you close and reopen the game your points will persist.
