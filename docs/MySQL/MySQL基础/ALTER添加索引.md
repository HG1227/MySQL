# ALTER添加索引

## 什么是索引？

索引用来快速地寻找那些具有特定值的记录，所有MySQL索引都以B-树的形式保存。如果没有索引，执行查询时MySQL必须从第一个记录开始扫描整个表的所有记录，直至找到符合要求的记录。表里面的记录数量越多，这个操作的代价就越高。如果作为搜索条件的列上已经创建了索引，MySQL无需扫描任何记录即可迅速得到目标记录所在的位置。如果表有1000个记录，通过索引查找记录至少要比顺序扫描记录快100倍。

MySQL中可以使用`alter table`这个SQL语句来为表中的字段添加索引。

## 添加索引 sql

1. 添加PRIMARY KEY（主键索引）

   ```sql
   alter table 'tablename' add primary key('column_name')
   ```

2. 添加`UNIQUE`(唯一索引)

   ```sql
   alter table 'table_name' add unique index index_name ('column')
   ```

3. 添加 `index` (普通索引)

   ```sql
   alter table 'table_name' add index index_name('column')
   ```

   例子：

   ```sql
   ALTER table t_debt_loan_log ADD INDEX debt_no ( `debt_no` ) 
   ```

4. 添加多列索引

   ```sql
   ALTER TABLE `table_name` ADD INDEX index_name ( `column1`, `column2`, `column3` )
   ```

5. 添加FULLTEXT(全文索引)

   ```sql
   ALTER TABLE `table_name` ADD FULLTEXT index  index_name ( `column`) 
   ```



## 索引所用的算法

唯一索引和普通索引使用的结构都是B-tree,执行时间复杂度都是O(log n)。



## 补充下概念：

### 1、普通索引

　　普通索引（由关键字KEY或INDEX定义的索引）的唯一任务是加快对数据的访问速度。因此，**应该只为那些最经常出现在查询条件（WHEREcolumn=）或排序条件（ORDERBYcolumn）中的数据列创建索引。**只要有可能，就应该选择一个数据最整齐、最紧凑的数据列（如一个整数类型的数据列）来创建索引。

### 2、唯一索引

　　普通索引允许被索引的数据列包含重复的值。比如说，因为人有可能同名，所以同一个姓名在同一个“员工个人资料”数据表里可能出现两次或更多次。
如果能确定某个数据列将只包含彼此各不相同的值，在为这个数据列创建索引的时候就应该用关键字UNIQUE把它定义为一个唯一索引。这么做的好处：一是简化了MySQL对这个索引的管理工作，这个索引也因此而变得更有效率；二是MySQL会在有新记录插入数据表时，自动检查新记录的这个字段的值是否已经在某个记录的这个字段里出现过了；如果是，MySQL将拒绝插入那条新记录。也就是说，唯一索引可以保证数据记录的唯一性。事实上，在许多场合，人们创建唯一索引的目的往往不是为了提高访问速度，而只是为了避免数据出现重复。

### 3、注意

经过实践发现，不要以为WHERE中的字段顺序无所谓，可以随便放在哪，应该尽可能地第一次就过滤掉大部分无用的数据，只返回最小范围的数据。

## 五、索引的缺点

到目前为止，我们讨论的都是索引的优点。事实上，索引也是有缺点的。
　　首先，**索引要占用磁盘空间。**通常情况下，这个问题不是很突出。但是，如果你创建每一种可能列组合的索引，索引文件体积的增长速度将远远超过数据文件。如果你有一个很大的表，索引文件的大小可能达到操作系统允许的最大文件限制。

　　第二，**对于需要写入数据的操作，比如DELETE、UPDATE以及INSERT操作，索引会降低它们的速度。**这是因为MySQL不仅要把改动数据写入数据文件，而且它还要把这些改动写入索引文件。



参考

- <a href="https://blog.csdn.net/u013421629/article/details/78622941" target="_blank">【mysql 索引】mysql 添加索引</a>