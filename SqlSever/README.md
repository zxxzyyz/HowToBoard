#Sql Server

### All databases in server
'''
SELECT Name FROM dbo.sysdatabases
```

### All tables in database
'''
SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_TYPE='BASE TABLE'
'''

### All tables in server
```
SET NOCOUNT ON
DECLARE @AllTables table (CompleteTableName nvarchar(4000))
INSERT INTO @AllTables (CompleteTableName)
    EXEC sp_msforeachdb 'select @@SERVERNAME+''.''+''?''+''.''+s.name+''.''+t.name from [?].sys.tables t inner join sys.schemas s on t.schema_id=s.schema_id'
SET NOCOUNT OFF
SELECT * FROM @AllTables ORDER BY 1
```
