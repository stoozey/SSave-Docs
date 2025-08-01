# SSave Manager

### `ssave_get`

#### Arguments

| Name              | Type       | Required? | Default                        | Description                              |
| ----------------- | ---------- | :-------: | ------------------------------ | ---------------------------------------- |
| `ssaveConstructor`| `Function` |  Yes      | —                              | The constructor for the SSave struct.    |
| `filePrefix`      | `String`   |   No      | `SSAVE_FILE_PREFIX_DEFAULT`    | Optional file prefix to use when loading. |

#### Returns

`Struct.SSave` – the requested (or newly created) save instance.

```js hl_lines="1""
var _save = ssave_get(SaveFile);
_save.set("foo", "bar");
```
