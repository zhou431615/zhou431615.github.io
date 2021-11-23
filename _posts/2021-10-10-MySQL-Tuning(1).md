---
layout:     post
title:      "MySQL调优(一)"
subtitle:   "MySQL学习笔记"
date:       2021-10-11 23:00:00
author:     "QianYe"

tags:
- Finance
---

## MySQL调优(一)（学习笔记）

> 学习笔记
>
> 1.为什么调优？（why）
>
> 2.“哪里”需要调优？（where)
>
> 3.优化原则  （How）

### 一、为什么要进行MySQL调优？

一般传统互联网公司很少接触到 SQL 优化问题，其原因是数据量小，大部分厂商的数据库性能能够满足日常的业务需求，所以不需要进行 SQL 优化，但是随着应用程序的不断变大，数据量的激增，数据库自身的性能跟不上了，此时就需要从 SQL 自身角度来进行优化。

从技术层面来说,   MySQL调优的好处有，

**避免网站页面出现访问错误**

1. 由于数据库练级timeout产生页面5xx错误
2. 由于慢查询造成页面无法加载
3. 由于阻塞造成数据无法提交

**增加数据库的稳定性**

1. 很多数据库问题都是由于低效的查询引起的

**优化用户的体验**

1. 流畅页面的访问速度
2. 良好的网站功能体验



从系统层面来说，MySQL调优的好处有，①调高系统的性能，②满足不断增加的业务需求。

> 般衡量一个项目的性能（这里指的是网站）的指标有三个：
>
> 吞度量：是单位时间内完成的用户或系统的请求数量。
> 并发数：同时可以去接收多少用户的访问请求。
> 响应时间：用户发出请求到收到响应的时间间隔。

### 二、排查SQL

> 排查当前的SQL，知道哪里需要优化。

当面对一个需要优化的 SQL 时，我们有哪几种排查思路呢？

1. ##### 通过 show status 命令 了解 SQL 执行次数

2. ##### 定位执行效率较低的 SQL语句

   ​      ：慢查询日志

   ​      ：Explain执行计划

------

#### 通过show status 命令了解SQL执行次数

首先，我们可以使用 **show status** 命令查看服务器状态信息。show status 命令会显示每个服务器变量 variable_name 和 value，状态变量是只读的。如果使用 SQL 命令，可以使用 like 或者 where 条件来限制结果。like 可以对变量名做标准模式匹配。

```sql
show status
```

![image-20211123115308671](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231747487.png)

这里需要注意一下 show status 命令中可以添加统计结果的级别，这个级别有两个

- session 级： 默认当前链接的统计结果
- global 级：自数据库上次启动到现在的统计结果

如果不指定统计结果级别的话，默认使用 session 级别。

对于 show status 查询出来的统计结果，有两类参数需要注意下，一类是以 `Com_` 为开头的参数，一类是以 `Innodb_` 为开头的参数。

下面是 Com_ 为开头的参数，参数很多。参数只展示部分。

```sql
show status like 'Com_%'
```

![image-20211123152854906](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231747237.png)

Com_xxx 表示的是每个 xxx 语句执行的次数，我们通常关心的是 select 、insert 、update、delete 语句的执行次数，即

- Com_select：执行 select 操作的次数，一次查询会使结果 + 1。
- Com_insert：执行 INSERT 操作的次数，对于批量插入的 INSERT 操作，只累加一次。
- Com_update：执行 UPDATE 操作的次数。
- Com_delete：执行 DELETE 操作的次数。

以 Innodb_ 为开头的参数主要有

- Innodb_rows_read：执行 select 查询返回的行数。
- Innodb_rows_inserted：执行 INSERT 操作插入的行数。
- Innodb_rows_updated：执行 UPDATE 操作更新的行数。
- Innodb_rows_deleted：执行 DELETE 操作删除的行数。

通过上面这些参数执行结果的统计，我们能够大致了解到当前数据库是以更新（包括插入、删除）为主还是查询为主。

除此之外，还有一些其他参数用于了解数据库的基本情况。

- Connections：查询 MySQL 数据库的连接次数，这个次数是不管连接是否成功都算上。
- Uptime：服务器的工作时间。
- Slow_queries：满查询次数。
- Threads_connected：查看当前打开的连接的数量。

![image-20211123153448961](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231747296.png)

> 更多的参数就不一一详解

总结一下，通过`show status` 命令，可以了解统计出SQL的执行次数，列举出所有的参数。

------

#### 定位执行效率较低的 SQL

定位执行效率比较慢的 SQL 语句，一般有两种方式

- 可以通过**慢查询日志**来定位哪些执行效率较低的 SQL 语句。
- 通过 **EXPLAIN** 命令分析 SQL 的执行计划

------

##### 可以通过**慢查询日志**来定位哪些执行效率较低的 SQL 语句

MySQL 中提供了一个慢查询的日志记录功能，可以把查询 SQL 语句时间大于多少秒的语句写入慢查询日志，日常维护中可以通过慢查询日志的记录信息快速准确地判断问题所在。用 --log-slow-queries 选项启动时，mysqld 会写一个包含所有执行时间超过 long_query_time 秒的 SQL 语句的日志文件，通过查看这个日志文件定位效率较低的 SQL 。

比如我们可以在 my.cnf 中添加如下代码，然后退出重启 MySQL。

```sql
log-slow-queries = /tmp/mysql-slow.log
long_query_time = 2
```

> 使用命令修改也是可行的；
>
> 如果使用云数据库，通过面板直接修改参数是非常方便的（阿里云&腾讯云）；

通常我们设置最长的查询时间是 2 秒，表示查询时间超过 2 秒就进行记录。通常情况下 2 秒就够了，然而对于很多 WEB 应用来说，2 秒时间还是比较长的。

也可以通过命令来开启：

先查询 MySQL 慢查询日志是否开启

```sql
show variables like "%slow%";
```

![image-20211123155157728](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231747418.png)

如未开器，开启慢查询日志。如已开始，无需此操作。

```sql
set global slow_query_log='ON';
```

> 如您的数据库部署到服务器，也可以通过宝塔面板直接修改参数；
>
> 修改注意权限问题，普通用户没有权限修改此类参数；

因为慢查询日志会在查询结束以后才记录，所以在应用反应执行效率出现问题的时候慢查询日志并不能定位问题，此时应该使用 **show processlist** 命令查看当前 MySQL 正在进行的线程。包括线程的状态、是否锁表等，可以实时的查看 SQL 执行情况。同样，使用**mysqladmin processlist**语句也能得到此信息。

```sql
show  peocesslist
```

![image-20211123162013678](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231747560.png)

下面就来解释一下各个字段对应的概念

- Id ：Id 就是一个标示，在我们使用 kill 命令杀死进程的时候很有用，比如 kill 进程号。
- User：显示当前的用户，如果不是 root，这个命令就只显示你权限范围内的 SQL 语句。
- Host：显示 IP ，用于追踪问题
- Db：显示这个进程目前连接的是哪个数据库，为 null 是还没有 select 数据库。
- Command：显示当前连接锁执行的命令，一般有三种：查询 query，休眠 sleep，连接 connect。
- Time：这个状态持续的时间，单位是秒
- State：显示当前 SQL 语句的状态，非常重要，下面会具体解释。
- Info：显示这个 SQL 语句。

> State 列非常重要，关于这个列的内容比较多，就不一一列举。

------

##### 通过 EXPLAIN 命令分析 SQL 的执行计划

> 什么是执行计划呢？简单来说，就是 SQL 在数据库中执行时的表现情况，通常用于 SQL 性能分析、优化和加锁分析等场景，执行过程会在 MySQL 查询过程中由解析器，预处理器和查询优化器共同生成。



##### MySQL 查询过程

如果能搞清楚 MySQL 是如何优化和执行查询的，不仅对优化查询一定会有帮助，还可以通过分析使用到的索引来判断最终的加锁场景。

下图是MySQL执行一个查询的过程。实际上每一步都比想象中的复杂，尤其优化器，更复杂也更难理解。

![](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231747840.png)



MySQL查询过程如下：

- 客户端发送一条查询给服务器。
- 服务器先检查查询缓存，如果命中了缓存，则立刻返回存储在缓存中的结果。否则进入下一阶段。
- 服务器端进行SQL解析、预处理，再由优化器生成对应的执行计划。
- MySQL根据优化器生成的执行计划，再调用存储引擎的API来执行查询。
- 将结果返回给客户端。



通过查询到效率低的 SQL 语句后，可以通过 EXPLAIN 或者 DESC 命令获取 MySQL 如何执行 SELECT 语句的信息，包括在 SELECT 语句执行过程中表如何连接和连接的顺序。

例如：某一条explain的SQL的执行计划

![image-20211123170137146](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748340.png)

> 对于DataGrip工具，选中SQL语句右键`Explain Plan (raw)`

我们可以看到，一个执行计划会展示12个相关的字段,下面我们对主要字段以及这些字段常见的值进行解释:

**id** :是一组数字，表示的是查询中执行select子句或者是操作表的顺序

规则：

1. id不相同的，id值越大越先执行
2. id相同的,从上到下顺序执行

**select_type**:

| 值           | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| SIMPLE       | 简单的SELECT语句（不包括UNION操作或子查询操作）              |
| PRIMARY      | 查询中最外层的SELECT（如两表做UNION或者存在子查询的外层的表操作为PRIMARY，内层的操作为UNION） |
| UNION        | UNION操作中，查询中处于内层的SELECT，即被union的SELECT       |
| SUBQUERY     | 子查询中的SELECT                                             |
| DERIVED      | 表示包含在 From 子句中的 Select 查询                         |
| UNION RESULT | union的结果,此时id为NULL                                     |

**table**: 涉及的表

**type**  ：

> type  重点了解

这列很重要,显示了连接使用哪种类型,有无使用索引， 常见的值从最好到最差如下 system > const > eq_ref > ref > range > index > all

| 值     | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| system | 表只有一行，MyISAM引擎所有                                   |
| const  | 常量连接，表最多只有一行匹配，通常用于主键或者唯一索引比较时,如: select * from t_user where id = 1; |
| eq_ref | 表关联查询时，对于前表的每一行,后表只有一行与之匹配。 (1) join查询 (2) 命中主键或者非空唯一索引 |
| ref    | 只使用了索引的最左前缀或者使用的索引是非唯一索引、非主键索引 |
| range  | between，in，>等都是典型的范围(range)查询                    |
| index  | 需要扫描索引上的全部数据,如: select count(*) from t_user;    |
| all    | 全表扫描                                                     |

> range ：**索引范围查询**，常见于使用 =，<>，>，>=，<，<=，IS NULL，<=>，BETWEEN，IN() 或者 like 等运算符的查询中。
>
> index ：索引全表扫描，把索引从头到尾扫一遍。
>
> all ： 这个我们接触的最多了，就是全表查询，select * from xxx ，性能最差。

**possible_keys**：表示可能用到的索引

**key**:表示最终用到的key

**ref**:显示索引的哪一列被使用了，有时候会是一个常量：表示哪些列或常量被用于查找索引列上的值

**rows**:估算出结果集行数，表示MySQL根据表统计信息及索引选用情况，估算的找到所需的记录所需要读取的行数, 原则上 rows 越少越好。

**filtered**:查询结果的行数占上面rows的百分比

**Extra**:

> Extra  重点了解

这一列也很重要,主要展示额外的信息说明,能够给出让我们深入理解执行计划进一步的细节信息

| 值                    | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| Using filesort        | 当order by 无法利用索引完成排序时,优化器不得不选择合适的算法从内存或者磁盘进行排序 |
| Using temporary       | 使用了临时表                                                 |
| Using index           | select后面的查询字段在索引中就可以取到,无需再回表了,即所谓的覆盖索引,这种查询性能很好 |
| Using index condition | mysql5.6之后引入了ICP(索引条件下推)                          |
| Using where           | Mysql 服务器在存储引擎检索行后再进行过滤                     |

------

### 三、优化原则

> 怎么进行优化
>
> 此处段落全文搬抄于好享家技术团队的文章。

通常有以下几种优化原则:

1. 让主要查询语句使用到合适的索引,type出现ALL(全表扫描)需格外注意,同时建立合适的索引以减少possible_keys的数量
2. type最好能达到ref级别
3. Extra列出现Using temporary、Using filesort（文件排序）务必去除

#### 优化思路

针对上面提到的几点优化原则,提供如下的优化思路

##### 针对优化原则1，2

上述1,2点其实都可以通过优化索引来达到目的,而要想让我们建的索引达到最优,则需要依据一个原则: 三星索引原则

简单描述就是

☆: where后条件匹配的索引列越多扫描的数据将越少

比如组合索引(a,b,c),最好在where后面能同时用到索引上的a,b,c这三列

☆: 避免再次排序

简单来说,就是排序字段尽量使用索引字段,因为索引默认是排好序的,使用索引字段排序可以避免再次排序

☆: 索引行包含查询语句中所有的列,即覆盖索引

基于这一点，我们应该少用select*来查询，以增加覆盖索引的可能性

如果你的索引能集齐上述三颗星,则说明你的索引是最优的索引！

##### 针对优化原则3

我们创建如下表，并插入一些数据

用户表

```
CREATE TABLE `t_user`  (
  `id` bigint(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `group_id` bigint(20) DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE,
  INDEX `idx_name`(`name`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1240277101395107842 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci ROW_FORMAT = Dynamic;
复制代码
```

分组表

```
CREATE TABLE `t_group`  (
  `id` bigint(20) NOT NULL,
  `group_name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci ROW_FORMAT = Dynamic;
复制代码
```

#### Using filesort

1. order by 的字段不在where条件中

   下面这条sql会出现Using filesort

   ```
   select * from t_user where group_id = 2 and age = 32 order by name;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748922.webp)



但是下面这条sql不会

   ```
   select * from t_user where group_id = 2 and age = 32 order by group_id ;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748954.webp)



2. 组合索引跨列

   举例:给t_user表创建索引(name,age,group_id)

   下面这条sql排序会出现Using filesort

   ```
   select * from t_user where name= '李A' order by group_id;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748199.webp)



但是下面这条就不会

   ```
   select * from t_user where name = '李A' order by age;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748671.webp)



因为第一条查询order by跳过了age,直接使用了group_id;删除索引(name,age,group_id);

3. 由于group by第一步默认进行了排序,所以当group by 的字段满足上述条件是,也会出现Using filesort,可以在group by后面加上order by null取消排序

#### Using temporary

临时表的出现对性能影响是很大的,主要会出现在以下情况中

1. 分组字段不在where条件后面,并且group by字段不是最终使用到的索引,原因有点类似于上面的Using filesort

   下面这条sql会出现Using temporary

   ```
   select * from t_user where group_id = 2 and name= '李A' group by age;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748732.webp)



但是下面这条sql不会

   ```
   select * from t_user where name = '李A' and age = 21 group by age;
   复制代码
   ```

**结论: where哪些字段,就group by 哪些字段**

2. 表连接中，order by的列不是驱动表中的

   如下sql是会创建临时表的

   ```
   explain select * from t_user t1 left join t_group t2 on t1.group_id = t2.id order by t2.id;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748844.webp)



因为t1和t2连接的时候,t1是驱动表,但是排序使用了被驱动表t2中的字段。改为t1的字段排序就不会出现临时表了,这里就不举例了。

**结论: 连接查询的时候，排序字段使用驱动表的字段**

3. order by和group by的子句不一样时

   ```
   explain select * from t_user group by group_id order by `name`;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748357.webp)



这种情况只能尽量使用同一个字段来分组和排序了，否则无法避免

4. distinct查询并且加上order by时

   ```
   explain select DISTINCT(`name`) from t_user order by age;
   复制代码
   ```



![执行计划](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111231748034.webp)



这种情况有时候无法避免，只能尽量将distinct的字段和order by的字段使用相同的索引。还有会出现临时表的情况有: from 中的子查询、union，这里就不一一举例了。

### 参考学习

[文章一](https://segmentfault.com/a/1190000040145951)

[文章二](https://segmentfault.com/a/1190000022939865)

[文章三](https://juejin.cn/post/6844903973032296461)







