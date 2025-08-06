# SSave Manager

## Functions

### **`ssave_get(ssaveConstructor, [filePrefix])`**

*This can only be used if the [`SSAVE_USE_MANAGER`](config.md#ssave_use_manager) configuration is `true`.*

Wrapper of [SSaveManager.get](ssave-manager.md#ssavemanagergetssaveconstructor-fileprefix).

---

### **`ssave_remove(ssaveConstructor, [filePrefix])`**

*This can only be used if the [`SSAVE_USE_MANAGER`](config.md#ssave_use_manager) configuration is `true`.*

Wrapper of [SSaveManager.remove](ssave-manager.md#ssavemanagerremovessaveconstructor-fileprefix).

---

### **`ssave_get_all([ssaveConstructor])`**

*Returns* `Array<`[`SSave`](ssave.md)`>` – an array of matching saves

| Name              | Type       | Required? | Default                        | Description                              |
| ----------------- | ---------- | :-------: | ------------------------------ | ---------------------------------------- |
| `ssaveConstructor`| `Function` |  No      | `Undefined`                     | The constructor for the SSave class.   |

*This can only be used if the [`SSAVE_USE_MANAGER`](config.md#ssave_use_manager) configuration is `true`.*

Iterates on all cached saves matching the constructor and returns an array of them.

If no constructor is supplied, ALL saves (regardless of their constructor), are returned.

---

## SSaveManager

### **`SSaveManager.get(ssaveConstructor, [filePrefix])`**

*Returns* [`SSave`](ssave.md) – the requested or created save instance

| Name              | Type       | Required? | Default                        | Description                              |
| ----------------- | ---------- | :-------: | ------------------------------ | ---------------------------------------- |
| `ssaveConstructor`| `Function` |  Yes      | —                              | The constructor for the SSave class.    |
| `filePrefix`      | `String`   |   No      | `SSAVE_FILE_PREFIX_DEFAULT`    | Optional file prefix to use when loading. Useful for things like save slots |

Looks for a cached save matching the constructor and prefix then returns it.
If it hasn't yet been cached, first, it will create one (and load it's contents if the file exists).

---

### **`SSaveManager.remove(ssaveConstructor, [filePrefix])`**

*Returns* `Undefined`

| Name              | Type       | Required? | Default                        | Description                              |
| ----------------- | ---------- | :-------: | ------------------------------ | ---------------------------------------- |
| `ssaveConstructor`| `Function` |  Yes      | —                              | The constructor for the SSave class.    |
| `filePrefix`      | `String`   |   No      | `SSAVE_FILE_PREFIX_DEFAULT`    | Optional file prefix to use when loading. Useful for things like save slots |

Looks for a cached save matching the constructor and prefix.
If it exists, it will be destroyed and removed from the cache.

---
