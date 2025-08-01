# SSave

<!-- SSave.load -->
## **`SSave.load([filePrefix])`**

---

*Returns* [`SSave`](ssave.md) – returns itself for chaining

| Name        | Type               | Required?  | Default  | Description                                                                                                              |
| --------    | -------------      | :-------:  | -------- | ------------------------------------------------------------------------------------------------------------------------ |
| `filePrefix`| `String` OR `Real` |  No        | `""`     | The prefix of the filename. Usually, you can leave this empty--but it can be useful for things like multiple save slots. |

Loads a save from disk.

<!-- SSave.set_protection -->
## **`SSave.set_protection(protection)`**

---

*Returns* [`SSave`](ssave.md) – returns itself for chaining

| Name        | Type                                            | Required? | Default  | Description                              |
| --------    | ----------                                      | :-------: | ---------| ---------------------------------------- |
| `protection`| [`SSAVE_PROTECTION`](enums.md#ssave_protection) |  Yes      | —        | The new protection level to set.    |

Updates the protection level of the file. This value gets cached, so you only need to call it once per change.

Don't worry about keeping track of/updating protection levels when loading files, this is handled automatically by SSave when [`load()`](ssave.md#ssaveloadfileprefix) is called.
