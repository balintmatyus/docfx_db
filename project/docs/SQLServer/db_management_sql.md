# DB Management Scripts

## User and db creatior stored proc.

``` sql
CREATE PROCEDURE CreateDatabaseAndUser
    @LoginName NVARCHAR(128),
    @DatabaseName NVARCHAR(128),
    @Password NVARCHAR(128)
AS
BEGIN
    -- Variable to hold the dynamic SQL statements
    DECLARE @sql NVARCHAR(MAX);

    -- Create the login
    SET @sql = 'CREATE LOGIN ' + QUOTENAME(@LoginName) + ' WITH PASSWORD = ''' + @Password + ''';';
    EXEC sp_executesql @sql;

    -- Create the database
    SET @sql = 'CREATE DATABASE ' + QUOTENAME(@DatabaseName) + ';';
    EXEC sp_executesql @sql;

    -- Create the user for the login in the database
    SET @sql = 'USE ' + QUOTENAME(@DatabaseName) + '; CREATE USER ' + QUOTENAME(@LoginName) + ' FOR LOGIN ' + QUOTENAME(@LoginName) + ';';
    EXEC sp_executesql @sql;

    -- Grant all privileges to the user on the database
    SET @sql = 'USE ' + QUOTENAME(@DatabaseName) + '; ALTER ROLE db_owner ADD MEMBER ' + QUOTENAME(@LoginName) + ';';
    EXEC sp_executesql @sql;

    PRINT 'Database and user created successfully.';
END;

Ebbe dobáltam bele a loginokat, adatbázisneveket és jelszavakat, pl:

EXEC CreateDatabaseAndUser
    @LoginName = 't1',
    @DatabaseName = 'db1',
    @Password = '27E6E222';
```

## Bulk user creation

``` sql
EXEC CreateDatabaseAndUser @LoginName = 't1', @DatabaseName = 'db1', @Password = '27E6E222';
EXEC CreateDatabaseAndUser @LoginName = 't2', @DatabaseName = 'db2', @Password = '1AE21E11';
EXEC CreateDatabaseAndUser @LoginName = 't3', @DatabaseName = 'db3', @Password = '68B3DF88';
EXEC CreateDatabaseAndUser @LoginName = 't4', @DatabaseName = 'db4', @Password = '173C394A';
EXEC CreateDatabaseAndUser @LoginName = 't5', @DatabaseName = 'db5', @Password = '0F1F0A9A';
EXEC CreateDatabaseAndUser @LoginName = 't6', @DatabaseName = 'db6', @Password = 'F2E454DF';
EXEC CreateDatabaseAndUser @LoginName = 't7', @DatabaseName = 'db7', @Password = '574F395C';
EXEC CreateDatabaseAndUser @LoginName = 't8', @DatabaseName = 'db8', @Password = '3A05DAE1';
EXEC CreateDatabaseAndUser @LoginName = 't9', @DatabaseName = 'db9', @Password = '9315268D';
EXEC CreateDatabaseAndUser @LoginName = 't10', @DatabaseName = 'db10', @Password = 'FA8CDD9D';
EXEC CreateDatabaseAndUser @LoginName = 't11', @DatabaseName = 'db11', @Password = '8E8AEF06';
EXEC CreateDatabaseAndUser @LoginName = 't12', @DatabaseName = 'db12', @Password = '95285970';
EXEC CreateDatabaseAndUser @LoginName = 't13', @DatabaseName = 'db13', @Password = '7CC2563D';
EXEC CreateDatabaseAndUser @LoginName = 't14', @DatabaseName = 'db14', @Password = '86B9DB9F';
EXEC CreateDatabaseAndUser @LoginName = 't15', @DatabaseName = 'db15', @Password = '3D184345';
EXEC CreateDatabaseAndUser @LoginName = 't16', @DatabaseName = 'db16', @Password = 'EEB91113';
EXEC CreateDatabaseAndUser @LoginName = 't17', @DatabaseName = 'db17', @Password = 'FDA2F3DA';
EXEC CreateDatabaseAndUser @LoginName = 't18', @DatabaseName = 'db17', @Password = 'E260E63B';
EXEC CreateDatabaseAndUser @LoginName = 't19', @DatabaseName = 'db19', @Password = '7584F61A';
EXEC CreateDatabaseAndUser @LoginName = 't20', @DatabaseName = 'db20', @Password = '12429939';
EXEC CreateDatabaseAndUser @LoginName = 't21', @DatabaseName = 'db21', @Password = '73F3F6F4';
EXEC CreateDatabaseAndUser @LoginName = 't22', @DatabaseName = 'db22', @Password = '7968E47C';
EXEC CreateDatabaseAndUser @LoginName = 't23', @DatabaseName = 'db23', @Password = '956C6BEC';
EXEC CreateDatabaseAndUser @LoginName = 't24', @DatabaseName = 'db24', @Password = '7A6A550D';
EXEC CreateDatabaseAndUser @LoginName = 't25', @DatabaseName = 'db25', @Password = '836F5F29';
```

## User deletion after the course

``` sql
CREATE PROCEDURE DropAllTablesAndConstraints
    @DatabaseName NVARCHAR(128)
AS
BEGIN
    DECLARE @sql NVARCHAR(MAX) = N'';

    -- Use the provided database
    SET @sql = 'USE ' + QUOTENAME(@DatabaseName) + ';';
    EXEC sp_executesql @sql;

    -- Drop all foreign key constraints
    SET @sql = N'';
    SELECT @sql += 'ALTER TABLE ' + QUOTENAME(s.name) + '.' + QUOTENAME(t.name)
        + ' DROP CONSTRAINT ' + QUOTENAME(f.name) + ';'
    FROM sys.foreign_keys AS f
    INNER JOIN sys.tables AS t
        ON f.parent_object_id = t.object_id
    INNER JOIN sys.schemas AS s
        ON t.schema_id = s.schema_id;

    EXEC sp_executesql @sql;

    -- Drop all tables
    SET @sql = N'';
    SELECT @sql += 'DROP TABLE ' + QUOTENAME(s.name) + '.' + QUOTENAME(t.name) + ';'
    FROM sys.tables AS t
    INNER JOIN sys.schemas AS s
        ON t.schema_id = s.schema_id;

    EXEC sp_executesql @sql;

    PRINT 'All tables and foreign key constraints have been dropped successfully.';
END;
```

