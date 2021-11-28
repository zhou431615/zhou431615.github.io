---
layout:     post
title:      "使用StarUML绘画E-R图"
subtitle:   "StarUML学习笔记"
date:       2021-10-03 08:00:00
author:     "QianYe"

tags:
- StarUML
---

## 使用StarUML绘画E-R图

### 定义

E-R图也称实体-联系图(Entity Relationship Diagram)，提供了表示实体类型、属性和联系的方法，用来描述[现实世界](https://baike.baidu.com/item/现实世界/688877)的[概念模型](https://baike.baidu.com/item/概念模型/3187025)。

### 作用

大部分数据库设计产品使用实体-联系模型（ER模型）**帮助用户进行数据库设计**。ER数据库设计工具提供了

一个“方框与箭头”的绘图工具，帮助用户建立ER图来描绘数据。（建立数据库表）

### 构图要素

成E-R图的3个基本要素是[实体型](https://baike.baidu.com/item/实体型)、属性和联系，其表示方法为：

1. 实体在E-R图中用**矩形**表示
2. 属性在E-R图中用**椭圆形**表示
3. 联系在E-R图中用**菱形**表示

### 一般性约束

实体-联系数据模型中的联系型，存在3种一般性约束：一对一约束（联系）、一对多约束（联系）和多对多约束（联系）

一般而言，传统普遍绘画的E-R的风格是如下这种：

![img](https://bkimg.cdn.bcebos.com/pic/267f9e2f07082838c4f1d7d0b899a9014d08f172?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2U4MA==,g_7,xp_5,yp_5/format,f_auto)

实体-联系数据模型中的联系型，存在3种一般性约束：一对一约束（联系）、一对多约束（联系）和多对多约束（联系），它们用来描述实体集之间的数量约束：

(1) 一对一联系(1 ∶1)

对于两个实体集A和B，若A中的每一个值在B中至多有一个实体值与之对应，反之亦然，则称实体集A和B具有一对一的联系。

一个学校只有一个正校长，而一个校长只在一个学校中任职，则学校与校长之间具有一对一联系。

[![img](https://bkimg.cdn.bcebos.com/pic/9213b07eca806538603965e29fdda144ac348274?x-bce-process=image/resize,m_lfit,w_294,limit_1/format,f_auto)](https://baike.baidu.com/pic/E-R图/304954/0/9213b07eca806538603965e29fdda144ac348274?fr=lemma&ct=single)

(2) 一对多联系(1 ∶N)

对于两个实体集A和B，若A中的每一个值在B中有多个实体值与之对应，反之B中每一个实体值在A中至多有一个实体值与之对应，则称实体集A和B具有一对多的联系。

例如，某校教师与课程之间存在一对多的联系“教”，即每位教师可以教多门课程，但是每门课程只能由一位教师来教。一个专业中有若干名学生，而每个学生只在一个专业中学习，则专业与学生之间具有一对多联系

(3) 多对多联系(M ∶N)

对于两个实体集A和B，若A中每一个实体值在B中有多个实体值与之对应，反之亦然，则称实体集A与实体集B具有多对多联系

[![img](https://bkimg.cdn.bcebos.com/pic/bba1cd11728b471072123c3dcbcec3fdfc032306?x-bce-process=image/resize,m_lfit,w_440,limit_1/format,f_auto)](https://baike.baidu.com/pic/E-R图/304954/0/bba1cd11728b471072123c3dcbcec3fdfc032306?fr=lemma&ct=single)

例如，表示学生与课程间的联系“选修 ”是多对多的，即一个学生可以学多门课程，而每门课程可以有多个学生来学。联系也可能有属性。例如，学生“ 选修” 某门课程所取得的成绩，既不是学生的属性也不是课程的属性。由于“ 成绩” 既依赖于某名特定的学生又依赖于某门特定的课程，所以它是学生与课程之间的联系“ 选修”的属性。

实际上，一对一联系是一对多联系的特例，而一对多联系又是多对多联系的特例。 [2] 联系是随着数据库语义而改变的，假如有如下3种语义规定：

例如，一个部门有一个经理，而每个经理只在一个部门任职，则部门与经理的联系是一对一的。

一个员工可以同时是多个部门的经理，而一个部门只能有一个经理，则这种规定下“员工”与“部门”之间的“管理”联系就是1：n的联系了。

一个员工可以同时在多个部门工作，而一个部门有多个员工在其中工作，则“员工”与“部门”的“工作”联系为m:n联系。 

### 弱实体

弱实体(weak entity)是一种[数据库系统](https://baike.baidu.com/item/数据库系统)术语。其定义为一个实体对于另一个实体（一般为强实体，也可以是依赖于其他强实体的弱实体）具有很强的依赖联系，而且该实体主键的一部分或全部从其强实体（或者对应的弱实体依赖的强实体）中获得，则称该实体为弱实体。（主键和外键）

------

### 使用StarUML 

了解基本的E-R概念，使用StarUML绘画E-R，可以生成DDL，定制个性样式，功能丰富。StarUML下载地址：http://staruml.io

![image-20211128145837665](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281458555.png)

当然还可以设置实体、连接线、图表的各种样式

![image-20211128151629593](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281516237.png)

绘制好E-R图，就可利用插件生成数据库的DDL。

> SQL语句主要可以划分为以下3个类别
>
> 　　**.**DDL(Data Definition Languages)语句：数据定义语言，这些语句定义了不同的数据段、数据库、表、列、索引等数据库对象。常用的语句关键字主要包括create、drop、alter等。
>
> 　　**.**DML(Data Manipulation Languages)语句：数据操纵语句，用于添加、删除、更新和查询数据库记录，并检查数据完整性。常用的语句关键字主要包括insert、delete、update和select等。
>
> 　　**.**DCL（Data Control Language）语句：数据控制语句，用于控制不同数据段直接的许可和访问级别的语句，这些语句定义了数据库、表、字段、用户的访问权限和安全级别，主要的语句关键字包括grant、revoke等。

其中在StarUML安装插件，使用离线安装。（因为某种网络原因，在线安装容易失败）

> This extension for StarUML ([http://staruml.io](http://staruml.io/)) support to generate DDL (Data Definition Language) from ERD. Install this extension from Extension Manager of StarUML.

官网地址：[StarUML](https://staruml.io/extensions)

![image-20211128152345495](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281523305.png)

### 安装流程

![image-20211128154430820](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281544457.png)

插件在github上的地址：[github.com](https://github.com/niklauslee/staruml-ddl)

 ![image-20211128155424935](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281554242.png)

### 使用插件

1. Click the menu (`Tools > DDL > Generate DDL...`)
2. Select a data model that will be generated to DDL.
3. Save the generated DDL to a file.

![image-20211128154707081](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281547851.png)

### DDL生成规则

Belows are the rules to convert from ERD elements to DDL.

- All entities and columns are converted to create table statements as follow:

```
CREATE TABLE entity1 (
    col1 INTEGER,
    col2 VARCHAR(20),
    ...
);
```

- Primary keys are converted as follow:

```
CREATE TABLE entity1 (
    pk1 INTEGER,
    pk2 VARCHAR(10),
    ...
    PRIMARY KEY (pk1, pk2, ...)
);
```

- Not-nullable columns are converted as follow:

```
CREATE TABLE entity1 (
    col1 VARCHAR(20) NOT NULL,
    ...
);
```

- Unique columns are converted as follow:

```
CREATE TABLE entity1 (
    ...
    UNIQUE (col1, col2, ...)
);
```

- Foreign keys are converted as follow:

```
CREATE TABLE entity1 (
    fk1 INTEGER,
    ...
);
...

ALTER TABLE entity1 ADD FOREIGN KEY (fk1) REFERENCES entity2(col1);
```

- If `Quote Identifiers` option is selected, all identifiers will be surrounded by a backquote character.

```
CREATE TABLE `entity1` (
    `col1` INTEGER,
    `col2` VARCHAR(20),
    ...
);
```

- If `Drop Tables` option is selected, drop table statements will be included.

(**MySQL** selected in `DBMS` option)

```
SET FOREIGN_KEY_CHECKS = 0;
DROP TABLE IF EXISTS entity1;
...
SET FOREIGN_KEY_CHECKS = 1;

CREATE TABLE entity1 (...);
...
```

(**Oracle** selected in `DBMS` option)

```
DROP TABLE entity1 CASCADE CONSTRAINTS;`
...

CREATE TABLE entity1 (...);
...
```

看一看生成的结果！

```sql
SET FOREIGN_KEY_CHECKS = 0;
DROP TABLE IF EXISTS `member`;
DROP TABLE IF EXISTS `memberlevel`;
DROP TABLE IF EXISTS `cart`;
DROP TABLE IF EXISTS `cartselectedmer`;
DROP TABLE IF EXISTS `category`;
DROP TABLE IF EXISTS `leaveword`;
DROP TABLE IF EXISTS `merchandise`;
DROP TABLE IF EXISTS `orders`;
DROP TABLE IF EXISTS `orderstatus`;
SET FOREIGN_KEY_CHECKS = 1;

CREATE TABLE `member` (
	`member` INTEGER NOT NULL,
	`memberLevel` INTEGER NOT NULL,
	`loginName` CHAR(12),
	`loginPwd` CHAR(12),
	`memberName` CHAR(20),
	`phone` CHAR(15),
	`address` VARCHAR(100),
	`zip` CHAR(10),
	`regDate` DATETIME,
	`lastDate` DATETIME,
	`loginTimes` INTEGER,
	`email` VARCHAR(100),
	PRIMARY KEY (`member`)
);
.....
```

### 扩展

阿里云中E-R图的画法    (云数据库)

![E-R](http://help-docs-aliyun.aliyuncs.com/assets/pic/47773/cn_zh/1480906901699/mysql.png)



Processon中的E-R图画法 （推荐使用）

![image-20211128163615367](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281636921.png)

Sybase PowerDesigner中的E-R图画法 （Outdated）

![image-20211128164604381](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281646889.png)

能绘画E-R的软件非常多,Visio、draw.io等，word甚至也可以画出简单的E-R图。具体到使用场景，哪个软件更方便，就用哪个。

### 
