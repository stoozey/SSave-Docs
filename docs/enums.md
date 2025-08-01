# Enums

## **`SSAVE_TYPE`**

Used to denote which type a save value uses.

- `STRING`
- `REAL`
- `BOOLEAN`
- `STRUCT`
- `ARRAY`
- `BUFFER`

---

## **`SSAVE_PROTECTION`**

Used to denote different levels of file protection.

- `NONE`
    - Save data is stored in plaintext json - good if you don't care about tampering (I highly recommend using this option!!)
- `ENCODE`
    - Save data is stored in base64 encoded json - good if you want *most* players to not know how to tamper
- `ENCRYPT`
    - Save data is encrypted with [`SSAVE_ENCRYPTION_KEY`](config.md#ssave_encryption_key) - good if you want *most* players to be unable to tamper. This is NOT secure enough for sensitive data

---
