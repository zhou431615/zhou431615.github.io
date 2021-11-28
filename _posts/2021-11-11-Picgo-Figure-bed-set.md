---
layout:     post
title:      "PicGo+阿里云OSS图床设置"
subtitle:   "图床教程"
date:       2021-11-11 13:00:00
author:     "QianYe"

tags:
- Typora
---

## PicGo+阿里云OSS图床设置

> 准备工作：
>
> - Typora (目前1.0以上版本开始收费,我的Version为0.9.98)  
> - Picgo    (Version:2.3.0) 
> - 开通阿里云OSS对象存储服务 （9元人民币/年 标准存储）
> - Picgo  下载地址 ：https://github.com/Molunerfinn/PicGo/releases
> - Picgo 插件下载地址：https://github.com/PicGo/Awesome-PicGo

### Intro

每次使用Typora写文章，记录学习笔记。虽然一时插入本地图片，随着本地的图片路径的更改，或者文件的缺失。原有的Markdown文档就无法查看图片。也就是说，即使将自己的文章分享给别人，别人也无法查看的你当时本地插入的图片。这种体验非常不好，于是为了解决Markdown中插入图片的问题，使用图床。那么图床是什么呢？图床一般是指储存图片的服务器，有国内和国外之分。国外的图床由于有空间距离等因素决定访问速度很慢影响图片显示速度。国内也分为单线空间、多线空间和cdn加速三种。我之前有利用Github作为免费的图床，但是访问速度慢，非常影响阅读体验。也有免费的图床，例如SM.MS,非常合适我目前写博客上传图片的需求，但是免费账号限额5GB，且没有中文技术生态。腾讯云的COS的计费模式复杂，且价格略贵；又拍云的USS计费模式是按量使用收费，价格便宜，非常合适这种博客图片上传。但是，综合考虑，未来的使用需求和产品的技术生态，我还是选择阿里云的OSS对象存储服务。

### 开通阿里云OSS

按包年包月购买

![image-20211128205559502](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282056286.png)

### 配置OSS

在控制台，创建Bucket (名字唯一，不可重复。因此，起一个有规则好记的名字)

![image-20211128210944180](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282109685.png)

创建文件夹，例如,Myblog/

![image-20211128211735212](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282117638.png)

配置授权，指定整个Bucket。

![image-20211128212353499](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282123384.png)

最后一步，获得Access ID 和Access Key，创建新的用户（指定获得单一权限，只能访问管理OSS资源）

![image-20211128213310017](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282133217.png)

赋予用户访问权限

![image-20211128213426943](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282134328.png)

最后，得到AccessID 和Access Key,可以下载CSV到本地保存，或者复制，以在后续的Picgo的图床配置中填写。这里就不赘述。

获得OSS的区域位置，例如oss-cn-beijing

![image-20211128214453262](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282144480.png)

### 配置Picgo

> 选用的Picgo版本最好使用稳定的，不要Beta版。（Beta版太多Bug）我目前使用Picgo  版本2.3.0

![image-20211128215038177](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282150360.png)

配置OSS

![image-20211128215433965](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282154808.png)

其他注意事项，如果不懂Server设置和代理设置，不要开启。随意开启，也可造成在Typora中无法访问查看图片（只显示一条链接）。到此就Picgo+OSS设置就基本完毕。

如果出现问题，请查看 issue #79 #86

------

如果想体验极佳的Typor编辑体验，可以参考我的后续设置。

既然是插入图片，关闭上传前重命名开关，以时间戳命名。（保持操作连贯，不要被打断）

![image-20211128221645225](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282216287.png)

其他设置，插件autocopy

![image-20211128215812858](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282215595.png)



### 关于Typora

偏好设置>>图像，设置图片插入图片就自动上传。

![image-20211128220429944](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282204012.png)

设置Markdown语法规则

![image-20211128222157210](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282221295.png)

### 拓展

其他图床介绍

SM.MS  开箱即用 https://sm.ms/   免费账号5GB

![image-20211128223056310](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282230499.png)

价格配置

![image-20211128223322416](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282233498.png)

又拍云  https://www.upyun.com/products/file-storage   计费模式单一，便宜。

![image-20211128223605434](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111282236531.png)

