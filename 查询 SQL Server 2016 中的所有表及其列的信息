要查询 SQL Server 2016 中的所有表及其列的信息，你可以使用系统视图来检索元数据。以下是查询所有表和列的 SQL 查询示例：

```sql
-- 查询所有表名和列名
SELECT 
    t.name AS TableName,
    c.name AS ColumnName
FROM sys.tables t
INNER JOIN sys.columns c ON t.object_id = c.object_id
ORDER BY TableName, ColumnName;
```

上述查询将返回所有表的名称以及它们的列名，按表名和列名的字母顺序排序。

如果你想查看更多表和列的详细信息，可以扩展查询，以包括其他相关信息，如数据类型、字符集合等：

```sql
-- 查询所有表的详细信息，包括列的数据类型和字符集合
SELECT 
    t.name AS TableName,
    c.name AS ColumnName,
    ty.name AS DataType,
    c.max_length AS MaxLength,
    c.collation_name AS Collation
FROM sys.tables t
INNER JOIN sys.columns c ON t.object_id = c.object_id
INNER JOIN sys.types ty ON c.user_type_id = ty.user_type_id
ORDER BY TableName, ColumnName;
```

这个查询将返回每个表的名称、列名、数据类型、最大长度和字符集合名称。

请注意，以上查询仅涵盖了表和列的基本信息。根据需要，你可以进一步扩展这些查询，以包括其他有关表和列的元数据信息。

------------------------------------------------------------
在 SQL Server 中，表的列的排序规则（collation）通常是在列的创建时指定的，可以在创建表或修改表的列时设置。排序规则会影响列的数据比较和排序行为。如果需要更改列的排序规则，你可以采取以下步骤：

1. 创建新列：首先，你可以创建一个具有所需排序规则的新列。

2. 复制数据：将现有列中的数据复制到新列中。你可以使用 INSERT INTO 语句来实现。

3. 更新应用程序：确保你的应用程序或查询使用新列而不是旧列。

4. 删除旧列：一旦你确定不再需要旧列，你可以删除它。

下面是一个示例 SQL 查询，用于创建一个新列并将数据从旧列复制到新列（请注意，下面的示例假设你要将排序规则从 `oldCollation` 更改为 `newCollation`）：

```sql
-- 步骤 1: 创建新列
ALTER TABLE YourTable
ADD NewColumnName NVARCHAR(MAX) COLLATE newCollation;

-- 步骤 2: 复制数据
INSERT INTO YourTable (NewColumnName)
SELECT OldColumnName
FROM YourTable;

-- 步骤 3: 更新应用程序

-- 步骤 4: 删除旧列（如果需要）
ALTER TABLE YourTable
DROP COLUMN OldColumnName;
```

请注意，这是一个涉及数据复制和列更改的操作，因此在执行之前务必小心，特别是在生产环境中。此外，你需要确保数据在复制期间不会丢失或损坏。备份数据库是一个明智的选择，以防意外发生。

总之，你可以手动更改表的列的排序规则，但这需要小心谨慎和一些额外的工作来确保数据的完整性和应用程序的兼容性。
