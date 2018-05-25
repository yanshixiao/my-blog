---
title: maven常用命令作用
date: 2018-04-26 15:43:56
categories: Java
tags: Java maven
---

#### maven常用命令的作用

1. mvn compile 编译,将Java 源程序编译成 class 字节码文件。
2. mvn test 测试，并生成测试报告。检查test方法中的断言是否为真，并在target中生成测试报告txt
3. mvn clean 将以前编译得到的旧的 class 字节码文件删除
4. mvn pakage 打包,动态 web工程打 war包，Java工程打 jar 包。
5. mvn install 将项目生成 jar 包放在仓库中，以便别的模块调用。jar包也有可能是war包，其路径及名称都取决于`pom.xml`文件中的配置，如：

```
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.chaboshi.web</groupId>
    <artifactId>com.chaboshi.web.www</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>war</packaging>
```
这样的配置，将会在maven仓库中生成如下文件

![](/images/java/java_1.jpg)

[传送门](https://www.cnblogs.com/ysocean/p/7416307.html)