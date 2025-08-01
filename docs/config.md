# Config

Located in `scr_ssave_config`, you can modify various options to your liking.

| Name                              | Type             | Description                                                                                                                                             |
|-----------------------------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SSAVE_DIRECTORY`                 | String           | The directory that saves are written to.                                                                                                                |
| `SSAVE_FILE_PREFIX_DEFAULT`       | String           | When no file prefix is defined (for the various functions that have an optional `filePrefix` argument), this value is used.                             |
| `SSAVE_USE_MANAGER`               | Boolean          | Whether or not the built-in SSaveManager implementation is used. Disable this if you dont need it, or you want to create your own version of it. |
| `SSAVE_PROTECTION_DEFAULT`        | SSAVE_PROTECTION | The default protection level used when [`set_protection`](ssave.md#ssaveset_protectionprotection) has not been already been called.                     |
| `SSAVE_ENCRYPTION_KEY`            | Real             | The encryption key used when save protection is set to [`SSAVE_PROTECTION.ENCRYPT`](enums.md#ssave_protection).                                         |
| `SSAVE_COPY_BUFFER_ON_SET`        | Boolean          | If true, when setting a buffer into a save value, this will copy the buffer so that you may safely delete the original.                                 |
| `SSAVE_ERROR_ON_SET_INVALID_TYPE` | Boolean          | If true, when setting a value with a type other than what was defined, throw an error. If false, a message is printed instead.                          |
