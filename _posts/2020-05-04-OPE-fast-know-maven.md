---
layout: post
title:  "一篇就够 | 快速理解什么是maven"
date:   2020-05-04 21:11:50 +0800
categories: onePostEnough
permalink: /:categories/:year/:month/:day/:title/
tags: 
- maven
- 实用
- 快速入门
excerpt_separator: <!--more-->
---

这篇文章会将笔者站在实用角度认为 maven 最重要的知识抽象提取出来，直击重点，从理论层面带你快速理解什么是 maven。<!--more-->

* 
{:toc}

## 一、maven介绍

### maven概念

maven是一个项目包管理工具，也是一种项目框架，满足maven项目结构规范的项目被称为maven项目。作为工具，maven可以用来完成外部工具包的导入，它的功能还远远高于管理包的导入：

* **管理外部依赖包的导入**：
在没接触过maven的开发者，相信很多人都有为导入外部依赖包的繁琐操作而烦恼。以连接 MySQL 数据库的 Java 依赖包为例，在先前刚学 JavaWeb 尚未接触 maven 时，若想添加 mysql-connector-java 工具包，要在网上把工具包下载下来，再通过IDE或者其他方式添加到开发项目里，其他工具也同样如此，如果需要更换版本，则得重新下载新版本的包文件再导入。
**如果使用 maven，事情会有很大不同。**每个 maven 项目都会有一个 pom.xml 文件（Project Object Model），导入工具包的过程将变为了修改 maven 项目的 pom.xml，在 \<dependencies\> 标签里面加入需导入工具包的 \<dependency\> 标签，可以在 [官方仓库](http://mvnrepository.com/){:target="_blank"} 网站搜索你需要的工具包的 \<dependency\>。需更改版本时，只改动 \<dependency\> 标签里面的 \<version\> 标签即可。
配置好 pom.xml 后，只需在 pom.xml 的路径中执行 `mvn install` ，即可将依赖包下载到本地仓库，集中管理，如果有项目需要用这个包，则直接从本地仓库里获取。同样具有这种功能的工具还有 Gradle、Ant。

* **功能远不止依赖包管理**：
maven 不仅仅可以为 maven 项目管理依赖包，它还可以将每个 maven 项目当作依赖包，甚至项目与项目之间还可以有面向对象特性的继承关系，每个项目是一个对象，项目里的所有内容是对象的属性，子项目可以继承父项目的所有内容。这样使得每个项目的独特性可以更强，项目与项目之间的耦合度可以很低 —— **像制作积木一样写项目，需要用时将积木拼凑起来构成应用。**
对于复用性非常强、对生产力提升很大的项目模块，甚至还可以上传到 maven 官方仓库让其他人也能享受便利，若不便公开，可以传至内部局域网的仓库（例如公司内网）。

### maven仓库

maven 在导入依赖包时，会按以下顺序在仓库中逐个寻找需要导入的包

* 本地仓库：当前计算机的 maven 仓库，默认会有一个专门的文件夹作为本地仓库
* 远程仓库：也被称为"内网仓库"，默认没有，可通过标签 \<repositories\> 进行配置
* 官方仓库：默认为 [官方仓库](http://mvnrepository.com/){:target="_blank"} ，可通过标签 \<mirrors\> 进行镜像设置，例如阿里云的maven官方仓库镜像 [https://maven.aliyun.com/](https://maven.aliyun.com/){:target="_blank"}

>[maven 官方文档 - 依赖引入优先级规则](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html){:target="_blank"}
>[Maven 项目中依赖的搜索顺序实验 - 云栖社区](https://yq.aliyun.com/articles/644131){:target="_blank"}
>
>结论：(检索项目依赖优先级) *local_repo > settings_profile_repo > pom_profile_repo > pom_repositories > settings_mirror > central*

### 生命周期

>maven官方文档：[入门指南 - 生命周期](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html){:target="_blank"}

以下是build一个项目时，可选的生命周期，也被称为"构建生命周期"，选择一个生命周期后，maven会按下方的顺序依次执行各个生命周期，直至所选的那个生命周期执行结束。例如如果选择了 `package`，则会从 `validate` 执行至 `package`，不需要进行后面的 `verify`、`install`、`deploy`。

* `validate` - 验证项目的结构是否正确
* `compile` - 编译项目源码
* `test` - 执行测试用例(如果有)，完成单元测试
* `package` - 将项目按配置的格式打包（常用）
* `verify` - 对集成测试的结果进行检查
* `install` - 将打好的包发布到本地仓库，供其他项目使用（常用）
* `deploy` - 将项目包发布到远程仓库，供其他开发者分享使用

除了上面的"构建生命周期"，maven还有另外两个生命周期指令，分别是：

* `clean` - 属于clean什么周期，用于清理项目已创建的所有文件（常用）
* `site` - 属于site什么周期，用于生成项目的文档（不常用）

### 使用方式

* 命令行操作，将maven的启动目录配置为环境变量，即可在任意路径下执行 mvn 指令了；
> [Maven常用命令 - cnblogs](https://www.cnblogs.com/wkrbky/p/6352188.html){:target="_blank"}
* 使用IDE创建maven项目，通过IDE的maven指令管理进行操作，主流的Java开发IDE都支持maven项目，这里不赘述细节；

>[Eclipse构建Maven项目 - 易百教程](https://www.yiibai.com/maven/m2eclipse-project.html){:target="_blank"}
>
>[在IDEA中创建maven项目](https://blog.csdn.net/zzy1078689276/article/details/78732183){:target="_blank"}


### 常见标签

#### \<groupId\>
位置：pom.xml<br>
作用：定义项目所在的组号，类似于java文件的package值<br>
举例 ：
```xml
<groupId>com.zty</groupId>
```
___

#### \<artifactId\>
位置：pom.xml<br>
作用：定义项目的名称，与groupId共同构成唯一的项目索引，类似于java文件的class值<br>
举例 ：
```xml
<artifactId>account</artifactId>
```
___

#### \<version\>
位置：pom.xml<br>
作用：定义项目的版本号，供项目的依赖者进行选择<br>
举例 ：
```xml
<version>1.1.0</version>
```
___

#### \<properties\>
位置：pom.xml<br>
作用：定义属性值，同一项目的其他地方可以通过EL表达式（${ }）来获取这些属性值的内容，这样做的目的是统一管理那些被多次使用的内容<br>
举例 ：
```xml
<version>${zty-framework.version}</version>
...
<properties>
  <zty-framework.version>0.8.1</zty-framework.version>
  <spring-web.version>5.2.3.RELEASE</spring-web.version>
  <fastjson.version>1.2.68</fastjson.version>
</properties>
```
___

#### \<parent\>
位置：pom.xml<br>
作用：声明当前项目继承的父项目，类似于java文件的extends，子项目将会继承父项目的所有内容，包括父项目的\<properties\><br>
举例 ：
```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.2.4.RELEASE</version>
</parent>
```
___

#### \<packaging\>
位置：pom.xml<br>
作用：声明当前项目的打包格式，默认值为jar，可选值为war、jar、pom<br>
举例 ：
```xml
<packaging>war</packaging>
```
___

#### \<module\>
位置：pom.xml - \<modules\><br>
作用：定义当前项目的子模块，必须与\<packaging\>pom\</packaging\>配套使用（所有被继承的项目的packaging必须为pom）<br>
举例 ：
```xml
<packaging>pom</packaging>
...
<modules>
  <module>wx</module>
  <module>file</module>
  <module>account</module>
  <module>redis</module>
  <module>wheel-gateway</module>
  <module>framework</module>
</modules>
```
___

#### \<repository\>
位置：setting.xml - \<repositories\><br>
作用：定义"远程仓库"，例如公司内部的maven仓库地址<br>
举例 ：
```xml
<repositories>
  <repository>
    <id>pom_repositories</id>
    <name>XX_Company</name>
    <url>http://10.18.29.128/nexus/content/groups/public/</url>
    <releases>
      <enabled>true</enabled>
    </releases>
    <snapshots>
      <enabled>true</enabled>
    </snapshots>
  </repository>
</repositories>
```
___

#### \<dependency\>
位置：pom.xml - \<dependencies\><br>
作用：用于指明需要引入的依赖<br>
举例 ：
```xml
<dependency>  
  <groupId>net.sf.json-lib</groupId>   
  <artifactId>json-lib</artifactId>   
  <version>2.2.2</version>
  <classifier>jdk15</classifier>
  <scope>compile</scope>  <!-- 可选值为： compile test provided runtime system -->
</dependency>  
```
___

#### \<plugins\>

位置：pom.xml - \<build\>或\<reporting\><br>
作用：指明用于覆盖maven默认操作的工具。maven指令的执行，其实也是基于插件进行的，maven有一套默认的官方插件，如果在项目pom.xml里引入plugins，执行maven指令操作时将会优先基于plugins的逻辑对项目进行操作，而不是maven默认的官方插件，例如Springboot打包的原理就是引入了专门的springboot-plugins。<build>对应于打包操作，<reporting>对应于报告。<br>
举例 ：
```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
  </plugins>
</build>
```
___


## 二、使用maven的最佳实践

关于使用maven的最佳实践，可参考我的另一篇文章：

> [一篇就够 \| 教你用maven搭建自己的开发框架](/onepostenough/2020/05/05/OPE-framework-base-on-maven/)

## 三、本文总结

从实用角度看，maven主要有两大核心作用：

1. 管理外部依赖包的导入；
2. 将项目做成依赖包，使我们可以使用面向对象思想管理项目；

___

#### 结尾

好的，“从实用角度快速理解maven”的所有内容到此正式结束了。[《一篇就够》](/tagSort/one-post-enough/) 系列是我沉淀各种知识整理而成的文章，只有沉淀到足够教会一个完全新人的程度我才会在里面写文章，每一篇都是我倾尽当时的所有才华所写的精品文章，欢迎常来逛逛哦。

![我的微信二维码](https://s1.ax1x.com/2020/05/13/YwZ2X6.jpg)

我是一个自我定位为“喜欢开发有趣工具的Java开发者"，如果对我的文章有任何疑惑或者想交流的地方，欢迎添加我的微信，二维码如上。
