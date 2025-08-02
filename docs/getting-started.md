# Getting Started

## Introduction

The purpose of this tool is to provide a simple way to manage saves and user settings in your project. Once you understand the basics, you can very easily integrate it into your games.

## Installation

Download the latest release from [GitHub](https://github.com/stoozey/SSave/releases) or [Itch.io](https://stoozey.itch.io/ssave).
In GameMaker, go to `Tools > Import Local Package` and select the downloaded `.yymps` file.

You'll see two folders: `SSave` and `Demo`. The demo includes a demonstration of the SSave system in use, if you aren't going to try it out, only worry about importing the `SSave` folder.

## Setting Up a SaveFile Class

Create a new script and inside it, add this code:

```js
function SaveFile() : SSave("save") {
    add_value("score", SSAVE_TYPE.REAL, 0);
}
```

This creates a new save file class that contains a score value.

When creating save classes, you need to extend the `SSave` class. This is so you can call the [`add_value()`](ssave.md#ssaveadd_valuename-type-default) method within it's constructor.

## Interfacing With the SaveFile Class

Before we start, create a new object and add this code to it:

```js title="Create Event"
// we will define these functions later
GetScore = function() { };
AddScore = function() { };
Save = function() { };
Load = function() { };

Load();
```

```js title="Step Event"
if (keyboard_check_pressed(vk_space)) {
    AddScore();
}

if (mouse_check_button_pressed(mb_left)) {
    Save();
}

if (mouse_check_button_pressed(mb_right)) {
    Load();
}
```

```js title="Draw Event"
var _score = GetScore();
draw_text(0, 0, $"Score: {_score}");
```

Now that we have this basic object set up, we can begin integrating it with with our `SaveFile` class.

---

When accessing save files, you have two options: manually creating save instances or allowing the [`SSaveManager`](ssave-manager.md) to handle it for you.

I recommend using the [`SSaveManager Method`](getting-started.md#ssavemanager-method) if you're just starting out, as it greatly simplifies the process of managing your saves.

### SSaveManager Method

First, we'll define the `Save` and `Load` functions:

```js title="Create Event"
Save = function() {
    var _save = ssave_get(SaveFile);
    _save.set("score", score);
    _save.save();
}

Load = function() {
    var _save = ssave_get(SaveFile);
    score = _save.get("score");
}
```

The bread-and-butter of this code is the [`ssave_get()`](ssave-manager.md#ssave_getssaveconstructor-fileprefix) function, which retrieves a persistent instance of the `SaveFile` class. If the save file doesn't exist, it will create one with the default values defined in the constructor.

Once you've called [`ssave_get()`](ssave-manager.md#ssave_getssaveconstructor-fileprefix) for the first time, the save class will be stored inside of the manager. Subsequent calls to [`ssave_get()`](ssave-manager.md#ssave_getssaveconstructor-fileprefix) will return this same instance, allowing you efficiently access and modify the save data from anywhere in your code without needing to load the file each time.

Lastly, we need to define the score functions:

```js title="Create Event"
GetScore = function() {
    return score;
}

AddScore = function() {
    score += 1;
}
```

---

### Manual Method

If we want to manage the save ourselves, we need to add a new variable to our object:

```js hl_lines="1" title="Create Event"
save = new SaveFile();

GetScore = function() { };
AddScore = function() { };
Save = function() { };
Load = function() { };

Load();
```

Next, we need to define the `Save` and `Load` functions:

```js title="Create Event"
Save = function() {
    save.save();
};

Load = function() {
    save.load();
}
```

And finally, the score functions:

```js title="Create Event"
GetScore = function() {
    return save.get("score");
}

AddScore = function() {
    var _newScore = GetScore() + 1;
    save.set("score", _newScore);
}
```

---

## Conclusion

If you test out your game now, you should be able to save via the left mouse button and load via the right mouse button. The score should increase when you press space. If you close the game and reopen it, your score will persist.
