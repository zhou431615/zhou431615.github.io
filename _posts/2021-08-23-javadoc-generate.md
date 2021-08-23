rake post title="javadoc生成" subtitle="Javadoc"

### Javadoc生成

- ##### javadoc命令生成

jaavadoc命令可以生成自己Api文档的，用文档注释+javaDoc命令即可生成

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


