# Config

Located in `scr_ssave_config`, you can modify various options to your liking.

## **`SSAVE_DIRECTORY`**

*Type:* `String`

The directory that saves are written to.

---

## **`SSAVE_FILE_PREFIX_DEFAULT`**

*Type:* `String`

When no file prefix is defined (for the various functions that have an optional `filePrefix` argument), this value is used.

---

## **`SSAVE_USE_MANAGER`**

*Type:* `Boolean`

When enabled, a persistant instance of [`SSaveManager`](ssave-manager.md) is created and can be used to manage saves via the [functions listed here](ssave-manager.md#functions).

---

## **`SSAVE_PROTECTION_DEFAULT`**

*Type:* [`SSAVE_PROTECTION`](enums.md#ssave_protection)

The default protection level used when [`set_protection`](ssave.md#ssaveset_protectionprotection) has not already been called.

---

## **`SSAVE_ENCRYPTION_KEY`**

*Type:* `Real`

The encryption key used when save protection is set to [`SSAVE_PROTECTION.ENCRYPT`](enums.md#ssave_protection).

---

## **`SSAVE_COPY_BUFFER_ON_SET`**

*Type:* `Boolean`

If true, when setting a buffer into a save value, this will copy the buffer so that you may safely delete the original.

---

## **`SSAVE_ERROR_ON_SET_INVALID_TYPE`**

*Type:* `Boolean`

If true, when setting a value with a type other than what was defined, throw an error. If false, a message is printed instead.

---
