If you are migrating virtual machines that were migrated in the past,
you must add the virtual machines to the migration plan with a CSV file,
because the migration plan cannot discover them automatically.

| Field      | Comments                                                                                 |
| ---------- | ---------------------------------------------------------------------------------------- |
| `Name`     | Virtual machine name. **Required**                                                       |
| `Host`     | **Optional**. Only required if virtual machines have identical `Name` fields.            |
| `Provider` | **Optional**. Only required if virtual machines have identical `Name` and `Host` fields. |

CSV file fields
