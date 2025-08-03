# SSave

## Constructor

### **`SSave([name, protection]) constructor`**

| Name     | Type                                              | Required? | Default                                                          | Description                              |
| -------- | ----------                                        | :-------: | ---------                                                        | ---------------------------------------- |
| `name`   | `String`                                           |  No      | `"data"`                                                         | The name of the file that gets written to disk. For example, the default value would save to disk as `data.ssave`.    |
| `protection`| [`SSAVE_PROTECTION`](enums.md#ssave_protection) |  No      | [`SSAVE_PROTECTION_DEFAULT`](config.md#ssave_protection_default) | The new protection level to set.    |

The constructor for the base SSave class. It is not intended to be used directly, but rather extended by other classes.

```js hl_lines="1" title="Defines a save file whose filename is 'save' and protection level is 'ENCODE'"
function SaveFile() : SSave("save", SSAVE_PROTECTION.ENCODE) constructor {
    // ...
}
```

---

### **`SSave.add_value(name, type, default)`**

*Returns* `Undefined`

| Name             | Type                                  | Required? | Default   | Description                              |
| --------         | ---------                             | :-------: | --------- | ---------------------------------------- |
| `name`           | `String`                              |  Yes      | -         | The name of the value.                   |
| `type`           | [`SSAVE_TYPE`](enums.md#ssave_type)   |  Yes      | -         | The type of the value.                   |
| `defaultValue`   | `Any`                                 |  Yes      | -         | The default value.                       |

This function is only intended to be used in the constructor when defining your save class.

```js hl_lines="2" title="Defines a value 'level' of type 'REAL' with a default value of 1"
function SaveFile() : SSave("save", SSAVE_PROTECTION.ENCODE) constructor {
    add_value("level", SSAVE_TYPE.REAL, 1);
}
```

---

## Class Functions

### **`SSave.load([filePrefix])`**

*Returns* [`SSave`](ssave.md) – returns itself for chaining

| Name        | Type               | Required?  | Default  | Description                                                                                                              |
| --------    | -------------      | :-------:  | -------- | ------------------------------------------------------------------------------------------------------------------------ |
| `filePrefix`| `String` OR `Real` |  No        | `""`     | The prefix of the filename. Usually, you can leave this empty--but it can be useful for things like multiple save slots. |

Loads a save from disk.

---

### **`SSave.save()`**

*Returns* `Boolean` – returns success

Saves the current state of the save to disk.

---

### **`SSave.get(name)`**

*Returns* `Any` – the current value

| Name     | Type       | Required? | Default   | Description                              |
| -------- | ---------- | :-------: | --------- | ---------------------------------------- |
| `name`   | `String`   |  Yes      | -         | The name of the value.              |

Retrieves the current value of the specified name. If the value does not exist, it will return the default value defined in [`add_value()`](ssave.md#ssaveadd_valuename-type-default).

---

### **`SSave.get_default(name)`**

*Returns* `Any` – the default value defined in [`add_value()`](ssave.md#ssaveadd_valuename-type-default).

| Name     | Type       | Required? | Default   | Description                 |
| -------- | ---------- | :-------: | --------- | --------------------------- |
| `name`   | `String`   |  Yes      | -         | The name of the value.      |

---

### **`SSave.set(name, value)`**

*Returns* [`SSave`](ssave.md) – returns itself for chaining

| Name      | Type       | Required? | Default   | Description                 |
| --------  | ---------- | :-------: | --------- | --------------------------- |
| `name`    | `String`   |  Yes      | -         | The name of the value.      |
| `value`   | `Any`      |  Yes      | -         | The new value to set.       |

---

### **`SSave.reset(name)`**

*Returns* [`SSave`](ssave.md) – returns itself for chaining

| Name      | Type       | Required? | Default   | Description                 |
| --------  | ---------- | :-------: | --------- | --------------------------- |
| `name`    | `String`   |  Yes      | -         | The name of the value.      |

Resets the value to its default as defined in [`add_value()`](ssave.md#ssaveadd_valuename-type-default).

---

### **`SSave.reset_all()`**

*Returns* [`SSave`](ssave.md) – returns itself for chaining

Resets all values to their defaults as defined in [`add_value()`](ssave.md#ssaveadd_valuename-type-default).

---

### **`SSave.set_protection(protection)`**

*Returns* [`SSave`](ssave.md) – returns itself for chaining

| Name        | Type                                            | Required? | Default  | Description                              |
| --------    | ----------                                      | :-------: | ---------| ---------------------------------------- |
| `protection`| [`SSAVE_PROTECTION`](enums.md#ssave_protection) |  Yes      | —        | The new protection level to set.    |

Updates the protection level of the save. This value gets cached, so you only need to call it once per change.

Don't worry about keeping track of/updating protection levels when loading files, this is handled automatically by SSave when [`load()`](ssave.md#ssaveloadfileprefix) is called.

---

### **`SSave.get_protection()`**

*Returns* [`SSAVE_PROTECTION`](enums.md#ssave_protection) – the current protection level

Returns the current protection level of the save.

---

### **`SSave.set_file_prefix(filePrefix)`**

*Returns* [`SSave`](ssave.md) – returns itself for chaining

| Name        | Type     | Required? | Default  | Description                    |
| --------    | -------- | :-------: | ---------| ------------------------------ |
| `filePrefix`| `String` |  Yes      | —        | The new file prefix to set.    |

Updates the file prefix of the save. This is useful for things like save slots, where you want to have multiple saves of the same ssave class.

---

### **`SSave.get_file_prefix()`**

*Returns* `String`

Returns the current file prefix of the save.

---

### **`SSave.get_full_name()`**

*Returns* `String`

Returns the file prefix and name of the save, which is the full filename that will be written to disk.

---
