  - Virtual machines are being migrated for the first time and are not
    discovered by the migration plan.
    
    Check that the source datastores and networks appear in the
    infrastructure mapping.

  - Previously migrated virtual machines cannot be discovered by the
    migration plan.
    
    Use a CSV file to add the virtual machines to the migration plan.

  - Virtual machines cannot be added to the migration plan with a CSV
    file.
    
    Check the CSV file format and fields. Create a new migration plan
    with the updated CSV file.

  - The **Create Migration Plan** wizard hangs while importing a CSV
    file.
    
    The CVS file is invalid, for example, virtual machines with a
    duplicate `Name` field and no `Host`/`Provider` field to distinguish
    them, or with a duplicate `Name` field and duplicate
    `Host`/`Provider` fields. Correct the CSV file, refresh the web
    page, and create a new migration plan.
