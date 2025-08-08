# task-1
## Fix Summary

- **Identified Issues:**
  - The application failed to start due to a `ScriptStatementFailedException` triggered by a SQL syntax error when inserting data into a table named `USER`, which is a reserved keyword in H2.
  - The `data.sql` script attempted to insert data before the table `User` was created, causing a `Table "User" not found` error.
  - `application.properties` had a formatting issue with `spring.datasource.initialization-mode` (spaces around the equals sign).
  - There was inconsistency between the JPA entity table name (`USER`) and the SQL script targeting `"USER"` or `"USER"`.

- **Fixes Applied:**
  - Quoted the table name in `data.sql` as `"USERS"` to ensure it matches the entity and avoid reserved keywords.
  - Ensured the `@Table(name = "USERS")` annotation in the `User` entity matches the table used in `data.sql`.
  - Removed `ddl-auto=update` and replaced it with a manually defined `schema.sql` to create the table before data is inserted.
  - Cleaned up the `application.properties` file by correcting the formatting of property keys and values.

- **Improvements and Recommendations:**
  - Renamed the table from `USER` to `users` or `app_user` to avoid using SQL reserved keywords and prevent similar issues on other databases like PostgreSQL or MySQL.
  - Recommended inserting seed data using a `DataInitializer` component in Java when relying on Hibernate to auto-generate schema (`ddl-auto=update`), to avoid timing issues with `data.sql`.
  - Suggested aligning naming conventions in code and SQL files to ensure better maintainability and readability.
