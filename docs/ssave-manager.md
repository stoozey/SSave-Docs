# SSave Manager

## Functions

### **`ssave_get(ssaveConstructor, [filePrefix])`**

Wrapper of [SSaveManager.get](ssave-manager.md#ssavemanagergetssaveconstructor-fileprefix).

This can only be used if the [`SSAVE_USE_MANAGER`](config.md#ssave_use_manager) configuration is `true`

---

### **`ssave_remove(ssaveConstructor, [filePrefix])`**

Wrapper of [SSaveManager.remove](ssave-manager.md#ssavemanagerremovessaveconstructor-fileprefix).

This can only be used if the [`SSAVE_USE_MANAGER`](config.md#ssave_use_manager) configuration is `true`

---

### **`ssave_get_all([ssaveConstructor])`**

*Returns* `Array<`[`SSave`](ssave.md)`>` – an array of matching saves

| Name              | Type       | Required? | Default                        | Description                              |
| ----------------- | ---------- | :-------: | ------------------------------ | ---------------------------------------- |
| `ssaveConstructor`| `Function` |  No      | `Undefined`                     | The constructor for the SSave class.   |

Iterates on all cached saves matching the constructor and returns an array of them.

If no constructor is supplied, ALL saves (regardless of their constructor), are returned.

This can only be used if the [`SSAVE_USE_MANAGER`](config.md#ssave_use_manager) configuration is `true`

---

## SSaveManager

### **`SSaveManager.get(ssaveConstructor, [filePrefix])`**

*Returns* [`SSave`](ssave.md) – the requested save instance

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
