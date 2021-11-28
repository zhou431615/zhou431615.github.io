---
layout:     post
title:      "UML作业总结"
subtitle:   "StarUML学习笔记"
date:       2021-09-16 08:10:00
author:     "QianYe"

tags:
- StarUML
---

@[TOC](UML作业)

 - [ ] 完善UML作业上各种UML图
 - [ ] 类图之间的各种关系
 - [ ] 图与代码的转化
 - [ ] 软件体系结构4+1UML图

### 用例图
一、某企业要建立一个生鲜配送网站，
该企业的需求如下:(共15分)
任意一个进入网站的人可以作为游客浏览该网站的生鲜商品；注册用户可以下订单、支付订单、查询订单、退换货，对于当前无货商品用户可以设定到货提醒; VIP用户在注册用户基础上可以购买专属商品。商品管理员可以对进行订单处理，普
通管理员可以调整增加、删除、修改商品;高级管理员可以设定管理员权限和账号。除浏览商品之外，系统所有功能均需要登录之后方可执行。
根据以上需求，回答下列问题:
A.该系统有哪些角色和用例， 他们之间的关系是什么。(5分）
B.冷所以上需求绘制用例图。(10分)
A.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201210215535575.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)

> 角色：游客、注册用户、VIP客户、商品管理员、普通管理员、高级管理员。
> 其关系：注册用户泛化于游客，VIP用户泛化于注册用户。普通管理员和高级管理员都泛化于游客。
> 用例：浏览网站、下订单、支付订单、查询订单、退换货、设定到货提醒、购买专属商品、订单处理、增加、删除、修改商品、设定管理员权限和账号、登录。
> 其关系：增加商品、删除商品、修改商品与浏览商品是扩展关系，登录被其他用例包含。

B.

> 有一个疑惑的地方，按照正常情况下。普通管理员和高级管理员应该都有浏览网站的功能。所以普通管理员和高级管理员都泛化于游客。注：UML用例图中泛化关系：子用例和父用例相似，但表现出更特别的行为；子用例将继承父用例的所有结构、行为和关系。子用例可以使用父用例的一段行为，也可以重载它。父用例通常是抽象的。在实际应用中很少使用泛化关系，子用例中的特殊行为都可以作为父用例中的备选流存在。


二、分析以下需求：某网络论坛系统，该系统的使用者包括：游客、注册用户、版主和管理员；游客仅可以浏览帖子，注册用户可以浏览帖子、发帖；版主不但可以浏览帖子、发帖，而且可以删除、查封、举报帖子；管理员可以管理讨论板块、管理用户权限；除了浏览帖子之外，所有功能均需要身份验证；用户发帖之后系统会对其内容进行检查，如果发现违禁内容则会自动向版主发邮件提醒。回答以下问题：
（1）系统包含哪些参与者，参与者之间关系是什么？
参与者：游客、注册用户、版主、管理员、系统，其中除系统之外参与者之间的关系是泛化关系。      版主继承注册用户和游客的功能，泛化关系。
（2）系统包含哪些用例，用例之间关系是什么？参与者与用例之间的关系是什么？
     用例：浏览帖子、发帖、删除帖子、查封帖子、举报帖子、管理讨论模块、管理用户权限、身份验证、内容检查、发邮件提醒。
     参与者与用例之间的关系：
      游客浏览帖子，关联关系；
      注册用户发帖，关联关系；
      版主查封帖子、删除帖子、举报帖子，关联关系；
      管理员管理讨论版块、管理用户权限，关联关系；
      发帖、查封帖子、删除帖子、举报帖子、管理讨论版块、管理用户权限都需要进行身份验证，包含关系；
      系统发邮件提醒，提供身份验证、内容检查， 关联关系；
用例之间的关系：
      发帖进行内容检查，包含关系；
      发帖、查封帖子、删除帖子、举报帖子、管理讨论版块、管理用户权限都需要进行身份验证，包含关系；
      内容检查与法邮件提醒，扩展关系。
      
（3）绘制用例图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201217233013238.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)


### 顺序图与协作图
一、对于问题1所描述述的生鲜配送网站，一个商品管理员处理订单的流程如下:(共20分)
商品管理员进入系统主界面，在主界面浏览已完成订单列表，主界面访问订单数据对象来查询订单列表，订单数据对象访问后台数据库，数据库获得订单信息返回给订单数据对象，订单数据对象将订单数据返回给主界面，主界面显示订单列表给商品管理员;商品管理员在主界面上选择特定订单，主界面显示订单详细信息，商品管理员在主界面上修改订单属性，主界面调用订单修改对象来修改订单属性，订单修改对象访问数据库实现数据修改，订单修改对象将修改结果返回给主界面，主界面向商品管理员现实修改的结果。

A.绘制该处理流程的顺序图。(10分)
B.绘制该处理流程的协作图。(10分)

> A.顺序图如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201210213203428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)

> B.协作图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201210223822319.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)


### 类图
三、对于订单管理某系统架构师设计了如下结构：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201120205617765.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
（1）系统中有哪些几个类，哪些类间有关系是什么(继承、组合、依赖)。(5分)
（2）使用程序设计语言(C++. Jana或C#)根据类图编写类的框架代码。(10分)
（3）编写一段代码，建立一个“淘宝订单”类的实例，并绘制对象图。 (5分)
答：
（1）
有商品类、水果类、蔬菜类、订单类、淘宝订单类、微信订单类、Location类、Status类、淘宝支付接口、微信支付接口。
继承关系：水果类、蔬菜类继承于商品类；淘宝订单类、微信订单类继承于订单类。
淘宝订单类实现淘宝支付接口，微信订单类实现微信支付接口。
Location、Statsu与订单呈关联类，商品聚合于订单类。
（2）Java实现的框架代码
```java
public abstract class 订单 {
    public String 订单名称;
    public Location 配送位置;
public void 支付() {}
public void 设置订单状态(status 状态) {}
}
public class 商品 {}
public class 蔬菜 extends 商品 {
    public void 新鲜度() {}
}
public class 水果 extends 商品 {
    public void 保质期() {}
}
public interface 淘宝支付接口 {}
public class 淘宝订单 extends 订单 {}
public interface 微信支付接口 {}
public class 微信订单 extends 订单 {}
public class Location {}
public class Status {}
C:“淘宝订单”类实例
Public class 淘宝订单 extends 淘宝支付{
淘宝订单 tb = new 淘宝订单（）;
tb.订单名称=“iMac mini”
tb.配送位置=“changchun”
}
```

> 注：利用StarUML的插件Java生成代码

(3)![在这里插入图片描述](https://img-blog.csdnimg.cn/20201120211644664.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
### 活动图
分析以下需求并绘制活动图。
一个网上订单管理的活动图文字描述如下：
(1)活动起始，用户下订单。
(2)系统并行进行处理： A生成送货单 B用户选择付款方式，如果超时未付款或者用户取消订单，订单取消活动终止；否则收款。
(3)供应商开始送货
(4)送货之后供货商修改订单中商品的状态。
(6)如果订单中所有商品均已送货完毕那么活动终止。
要求绘制完整的活动图。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213221248649.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)

### 状态图
分析以下需求并绘制状态图
一个电商的订单系统：
订单生成，订单取消（用户自主取消或者缴费期限已过）。备货中（用户缴费）；出货中（库存量足够）或出货失败（超期之后库存仍然不足）；出货完毕（子状态：成功减掉库存、发送货物、添加邮寄信息）；收货完毕（用户签收货物）；订单完成（用户确认收货）；

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201219141157569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)


### 包图
系统的源代码分成多个包：界面显示包、业务逻辑包、数据访问包和底层控制包；界面显示包、业务逻辑包、数据访问包依赖于底层控制包，绘制对应的包图；
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020121410591115.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)

### 组件图
系统的数据分析部分包含多种组件，分别为基础数据访问组件、数理统计组件、大数据分析组件、决策支持组件；所有组件均依赖于数据访问组件，此外决策支持组件还依赖于大数据分析组件，绘制对应的组件图；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201214111857510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)

### 部署图
使用Web服务器（使用Tomcat）、数据服务器（Hadoop）在内部网上部署系统，客户端通过浏览器（IE）访问系统，Web服务器连接打印机实现报表打印，绘制系统的部署图。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201214111944662.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
## UML类图关系
类图之间的关系众说纷纭，但大体一致。
#### docs.staruml.io
参照[https://docs.staruml.io/working-with-uml-diagrams/class-diagram#relationship](https://docs.staruml.io/working-with-uml-diagrams/class-diagram#relationship)
Relationship is an abstract element representing a relationship between UML elements.
Subclasses of Relationship are:
Generalization  泛化
Association   关联
Aggregation  聚合
Composition  组合
Dependency   依赖
Interface Realization  接口实现
Component Realization  组件实现
Include   包含
Exclude  排除
#### Java设计模式附录A.3
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020121915190264.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201219153401872.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
> 参考借鉴：[UML类图总结](https://blog.csdn.net/ibukikonoha/article/details/80643959)
## UML中“4+1”视图模型描述软件体系结构
![4+1视图](https://img-blog.csdnimg.cn/20210201220559471.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDIyOTI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
分别有逻辑视图、发展视图、进程视图、物理视图、场景视图。
参考[4+1视图与UML对应关系](https://www.cnblogs.com/I-am-Betty/p/5467847.html)
[Architectural Blueprints—The “4+1” View
Model of Software Architecture](https://www.cs.ubc.ca/~gregor/teaching/papers/4+1view-architecture.pdf)
