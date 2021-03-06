# IS NULL语句

## NULL：空值查询

MySQL 提供了 `IS NULL `关键字，用来判断字段的值是否为空值（`NULL`）。**空值不同于 0，也不同于空字符串**。

如果字段的值是空值，则满足查询条件，该记录将被查询出来。如果字段的值不是空值，则不满足查询条件。

使用 IS NULL 的基本语法格式如下：

> IS [NOT] NULL

其中，“`NOT`”是可选参数，表示字段值不是空值时满足条件。



下面使用` IS NULL `关键字来查询 tb_students_info 表中 login_date 字段是 `NULL` 的记录。

```sql
mysql> SELECT `name`,`login_date` FROM tb_students_info 
    -> WHERE login_date IS NULL;
+--------+------------+
| NAME   | login_date |
+--------+------------+
| Dany   | NULL       |
| Green  | NULL       |
| Henry  | NULL       |
| Jane   | NULL       |
| Thomas | NULL       |
| Tom    | NULL       |
+--------+------------+
6 rows in set (0.01 sec)
```


注意：IS NULL 是一个整体，不能将 IS 换成“=”。如果将 IS 换成“=”将不能查询出任何结果，数据库系统会出现“Empty set(0.00 sec)”这样的提示。同理，IS NOT NULL 中的 IS NOT 不能换成“!=”或“<>”。

`IS NOT NULL` 表示查询字段值不为空的记录。



下面使用 IS NOT NULL 关键字来查询 tb_students_info 表中 login_date 字段不为空的记录。

```sql
mysql> SELECT `name`,login_date FROM tb_students_info 
    -> WHERE login_date IS NOT NULL;
```



