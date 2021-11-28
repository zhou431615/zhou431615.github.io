---
layout:     post
title:      "IDEA中如何生成Javadoc"
subtitle:   "Javadoc生成"
date:       2021-08-23 21:00:00
author:     "QianYe"

tags:
- Java
---

### Javadoc生成

- ##### javadoc命令生成

Javadoc命令可以生成自己Api文档的，用文档注释+javaDoc命令即可生成

```
 F:>javadoc -encoding UTF-8 -charset UTF-8 Doc.java 
```

- ##### 用IDE（idea）生成

  选项栏=>Tools=>Generate JavaDoc

  参数说明 ：

  - Whole project 整个项目都生成
  - Custom scope 自定义范围，说明：
    - project files 项目文件
    - project production files 项目产品文件
    - project test files 项目的测试文件
    - class hierarchy 类层
  - include test source 包含测试目录
  - include JDK and... 包含jdk和其他的第三方jar
  - link to JDK documentation… 链接到JDK api
  - output directy 生成的文档存放的位置（必选）
  - 左边滑动栏 private、package、protected、public 生成文档的级别（类和方法）
  - 中间多选栏 Generate * 是选择生成的文档包含的内容，层级树、导航、索引
  - 右边多选栏 生成的文档包含的内容信息，作者、版本等信息
  - Locale 语言类型，例如：zh-CN
  - Other command line arguments 其他参数，例如：-encoding UTF-8 -charset UTF-8
  - Maximum heap size 生成文档大小限制
  - 选择OK

  #### **参数**
  
  - @author 作者名
  - @version 版本号
  - @since 指明需要最早使用的JDK版本
  - @param 参数名
  - @return 返回值情况
  - @throws 异常抛出情况
  
     <img src="https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281306436.png" alt="image-20211128130619931"  />
  
  
  
  #### 说明：（踩坑记录）
  
  -   第一个坑：IDEA生成javadoc文档时无法访问FileSystem报错
  
  ```
  正在构造 Javadoc 信息…
  D:\Environment\jdk1.8.0_131\src.zip(java/nio/file/Path.java):106: 错误: 无法访问FileSystem
  FileSystem getFileSystem();
  ^
  错误的源文件:D:\Environment\jdk1.8.0_131\src.zip(java/nio/file/FileSystem.java)
  文件不包含类java.nio.file.FileSystem
  请删除该文件或确保该文件位于正确的源路径子目录中。
  1 个错误
  ```
  
  #####   解决办法：
  
  1. 根据它的提示，找到jdk文件中的src压缩包
  2. 解压这个压缩包到jdk文件中
  3. 删除src压缩包
  4. 重启IDEA，重新生成javadoc文件
  5. 记得输入-encoding utf-8 -charset utf-8
  
  
  
  -  第二个坑：Javadoc生成文档时java.lang.IllegalArgumentException报错
  
  ```
  java.lang.IllegalArgumentException 
  
       at sun.net.www.ParseUtil.decode(ParseUtil.java:202) 
  
       at sun.misc.URLClassPath$FileLoader.<init>(URLClassPath.java:1016) 
  
       at sun.misc.URLClassPath$3.run(URLClassPath.java:357) 
  
       at sun.misc.URLClassPath$3.run(URLClassPath.java:352) 
  
       at java.security.AccessController.doPrivileged(Native Method) 
  
       at sun.misc.URLClassPath.getLoader(URLClassPath.java:351) 
  
       at sun.misc.URLClassPath.getLoader(URLClassPath.java:328) 
  
       at sun.misc.URLClassPath.findResource(URLClassPath.java:171) 
       .......
  ```
  
  ##### 出现原因：
  
  环境变量中classpath里面字符冲突引起的。classpath中包含了%JAVA_HOME%\lib;
  
  ##### 解决方法：
  
  是重新设置classpath或者删除classpath。设置完成后重启生效！

### 生成Javadoc文档

javadoc 工具将你 Java 程序的源代码作为输入，输出一些包含你程序注释的HTML文件。

每一个类的信息将在独自的HTML文件里。javadoc 也可以输出继承的树形结构和索引。

由于 javadoc 的实现不同，工作也可能不同，你需要检查你的 Java 开发系统的版本等细节，选择合适的 Javadoc 版本。

![image-20211128131948142](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111281319949.png)




