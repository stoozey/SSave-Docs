# Examples

## Using SSave Without the Manager

While the [`SSaveManager`](ssave-manager.md) is a convenient, hands-off way to handle and cache saves, you may find yourself wanting more control.

Assuming you have a `SaveFile` class like this:

```js
function SaveFile() : SSave() {
    // ...
}
```

Instead of using [`ssave_get()`](ssave-manager.md#ssave_getssaveconstructor-fileprefix), you can directly create an instance of `SaveFile` and manage it manually:

```js
var _save = new SaveFile();
_save.load();
```

Using the `new` operator will create an empty `SaveFile` instance. Now you can call [`load()`](ssave.md#ssaveloadfileprefix) to populate it with data from disk, or [`save()`](ssave.md#ssavesave) to write the current state to disk as usual.

You'll likely need to create some kind of persistent object/script to store your saves, else you will incur a performance pentaly by constantly loading your save every time you need it.
