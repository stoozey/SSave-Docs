# Examples

## Using SSave Without the Manager

While the [`SSaveManager`](ssave-manager.md) is a convenient, hands-off way to handle saves, you may find yourself wanting more control.

Assuming you have a `SaveFile` class like this:

```js
function SaveFile() : SSave() {
    add_value("score", SSAVE_TYPE.REAL, 0);
}
```

Instead of using functions like `ssave_get()`, you can directly create an instance of `SaveFile` and manage it manually:

```js
var _save = new SaveFile();
```

This will create an empty `SaveFile` instance. Now you can call [`load()`](ssave.md#ssaveloadfileprefix) to populate it with data from disk, or [`save()`](ssave.md#ssavesave) to write the current state to disk.
