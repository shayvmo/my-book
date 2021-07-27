## Explain 命令

2020年12月23日



[参考地址](https://www.cnblogs.com/tufujie/p/9413852.html)



### 日常开发必备操作

1、日常开发，`mysql`数据库的慢日志先打开，并设置查询时间为1秒。

2、开启 `binlog`



【建议】在开发阶段，预先分析一下查询语句是否使用索引，查询字段是否为 * 等等



### Explain 比较重要的字段

- type
- select_type 
- key
- rows



#### select_type

-  `SIMPLE` 
  - (简单SELECT，不使用UNION或子查询等)

- ` PRIMARY `
  - (子查询中最外层查询，查询中若包含任何复杂的子部分，最外层的select被标记为PRIMARY)

- ` UNION` 
  - (UNION中的第二个或后面的SELECT语句)

- `DEPENDENT UNION`
  - (UNION中的第二个或后面的SELECT语句，取决于外面的查询)

- `UNION RESULT`
  - (UNION的结果，union语句中第二个select开始后面所有select)

- `SUBQUERY`
  - (子查询中的第一个SELECT，结果不依赖于外部查询)

- `DEPENDENT SUBQUERY`
  - (子查询中的第一个SELECT，依赖于外部查询)

- `DERIVED`
  - (派生表的SELECT, FROM子句的子查询)

- `UNCACHEABLE SUBQUERY`
  - (一个子查询的结果不能被缓存，必须重新评估外链接的第一行)

 

#### type

对表访问方式，表示MySQL在表中找到所需行的方式，又称“访问类型”。

常用的类型有： **ALL、index、range、 ref、eq_ref、const、system、NULL（从左到右，性能从差到好)**

- `ALL`
  - Full Table Scan， MySQL将遍历全表以找到匹配的行

- `index`
  - Full Index Scan，index与ALL区别为index类型只遍历索引树

- `range`
  - 只检索给定范围的行，使用一个索引来选择行

- `ref`
  - 表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值

- `eq_ref`
  - 类似ref，区别就在使用的索引是唯一索引，对于每个索引键值，表中只有一条记录匹配，简单来说，就是多表连接中使用primary key或者 unique key作为关联条件

- `const`、`system`
  - 当MySQL对查询某部分进行优化，并转换为一个常量时，使用这些类型访问。如将主键置于where列表中，MySQL就能将该查询转换为一个常量，system是const类型的特例，当查询的表只有一行的情况下，使用system

- `NULL`
  - MySQL在优化过程中分解语句，执行时甚至不用访问表或索引，例如从一个索引列里选取最小值可以通过单独索引查找完成



#### key 

key列显示MySQL实际决定使用的（索引），必然包含在possible_keys中



#### rows 

预估需要读取多少行才能找到需要的记录
