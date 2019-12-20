# Sql Server

### All databases in a server
```
SELECT Name FROM dbo.sysdatabases
```

### All tables in a database
```
SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_TYPE='BASE TABLE'
```

### All tables in a server
```
SET NOCOUNT ON
DECLARE @AllTables table (CompleteTableName nvarchar(4000))
INSERT INTO @AllTables (CompleteTableName)
    EXEC sp_msforeachdb 'select @@SERVERNAME+''.''+''?''+''.''+s.name+''.''+t.name from [?].sys.tables t inner join sys.schemas s on t.schema_id=s.schema_id'
SET NOCOUNT OFF
SELECT * FROM @AllTables ORDER BY 1
```

### Columns to csv
```
Select TABLE_SCHEMA, TABLE_NAME
, Stuff(
(
Select ',' + C.COLUMN_NAME
From INFORMATION_SCHEMA.COLUMNS As C
Where C.TABLE_SCHEMA = T.TABLE_SCHEMA
    And C.TABLE_NAME = T.TABLE_NAME
Order By C.ORDINAL_POSITION
For Xml Path('')
), 1, 1, '') As Columns
From INFORMATION_SCHEMA.TABLES As T
WHERE T.TABLE_NAME='TableName'
```

### Generate ADO .net parameters
```
SELECT 'cmd.Parameters.AddWithValue("@'+COLUMN_NAME+'", '+COLUMN_NAME+');'
FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME='TableName'; 
```

### Paging tables
```
SELECT * FROM (SELECT  ROW_NUMBER() OVER(ORDER BY @Order) AS RowNum,* FROM @Table)as Result
WHERE RowNum>=20 AND RowNum<=40
ORDER BY RowNum
```

### Recently excuted queries
```
SELECT qp.query_plan, deqs.last_execution_time AS [Time], dest.text AS [Query], dest.*
FROM sys.dm_exec_query_stats AS deqs
CROSS APPLY sys.dm_exec_sql_text(deqs.sql_handle) AS dest
CROSS APPLY sys.dm_exec_query_plan(plan_handle) as qp
ORDER BY deqs.last_execution_time DESC
```

### Count of all tables in database
```
create table #tempcount (tablename nvarchar(128), record_count bigint)
EXEC sp_msforeachtable 'insert #tempcount select ''?'', count(*) from ? with (nolock)'
select * from #tempcount
drop table #tempcount



SELECT
      QUOTENAME(SCHEMA_NAME(sOBJ.schema_id)) + '.' + QUOTENAME(sOBJ.name) AS [TableName]
      , SUM(sPTN.Rows) AS [RowCount]
FROM 
      sys.objects AS sOBJ
      INNER JOIN sys.partitions AS sPTN
            ON sOBJ.object_id = sPTN.object_id
WHERE
      sOBJ.type = 'U'
      AND sOBJ.is_ms_shipped = 0x0
      AND index_id < 2 -- 0:Heap, 1:Clustered
GROUP BY 
      sOBJ.schema_id
      , sOBJ.name
ORDER BY [TableName]



SELECT 
[TableName] = so.name, 
    [RowCount] = MAX(si.rows) 
FROM 
    sysobjects so, 
    sysindexes si 
WHERE 
    so.xtype = 'U'
    AND 
    si.id = OBJECT_ID(so.name) 
GROUP BY 
    so.name 
ORDER BY 
    2 DESC 
```

### Search for column
```
SELECT c.name AS ColName, t.name AS TableName
FROM sys.columns c
JOIN sys.tables t ON c.object_id = t.object_id
WHERE c.name LIKE '%ColumnName%' 
```

### Search for string in all tables
```
DECLARE @SearchStr nvarchar(100)='string'
CREATE TABLE #Results (ColumnName nvarchar(370), ColumnValue nvarchar(3630))

SET NOCOUNT ON
 
DECLARE @TableName nvarchar(256), @ColumnName nvarchar(128), @SearchStr2 nvarchar(110)
SET  @TableName = ''
SET @SearchStr2 = QUOTENAME('%' + @SearchStr + '%','''')
 
WHILE @TableName IS NOT NULL
 
BEGIN
    SET @ColumnName = ''
    SET @TableName = 
    (
        SELECT MIN(QUOTENAME(TABLE_SCHEMA) + '.' + QUOTENAME(TABLE_NAME))
        FROM     INFORMATION_SCHEMA.TABLES
        WHERE         TABLE_TYPE = 'BASE TABLE'
            AND    QUOTENAME(TABLE_SCHEMA) + '.' + QUOTENAME(TABLE_NAME) > @TableName
            AND    OBJECTPROPERTY(
                    OBJECT_ID(
                        QUOTENAME(TABLE_SCHEMA) + '.' + QUOTENAME(TABLE_NAME)
                         ), 'IsMSShipped'
                           ) = 0
    )
 
    WHILE (@TableName IS NOT NULL) AND (@ColumnName IS NOT NULL)
 
    BEGIN
        SET @ColumnName =
        (
            SELECT MIN(QUOTENAME(COLUMN_NAME))
            FROM     INFORMATION_SCHEMA.COLUMNS
            WHERE         TABLE_SCHEMA    = PARSENAME(@TableName, 2)
                AND    TABLE_NAME    = PARSENAME(@TableName, 1)
                AND    DATA_TYPE IN ('char', 'varchar', 'nchar', 'nvarchar', 'int', 'decimal')
                AND    QUOTENAME(COLUMN_NAME) > @ColumnName
        )
 
        IF @ColumnName IS NOT NULL
 
        BEGIN
            INSERT INTO #Results
            EXEC
            (
                'SELECT ''' + @TableName + '.' + @ColumnName + ''', LEFT(' + @ColumnName + ', 3630) 
                FROM ' + @TableName + 'WITH (NOLOCK) ' +
                ' WHERE ' + @ColumnName + ' LIKE ' + @SearchStr2
            )
        END
    END    
END
 
SELECT ColumnName, ColumnValue FROM #Results
DROP TABLE #Results
```
