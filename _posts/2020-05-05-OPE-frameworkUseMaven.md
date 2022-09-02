---
layout: post
title:  "一篇就够 | 教你用maven搭建自己的开发框架"
date:   2020-05-05 19:39:10 +0800
categories: onePostEnough
permalink: /:categories/:year/:month/:day/:title/
tags: 
- 自制框架
- maven最佳实践
- Spring
excerpt_separator: <!--more-->
---

这篇文章先会讨论什么是"框架"，然后向你展示一个基于 maven 特性搭建的自制开发框架与该框架的使用示例，最后将这个自制框架的搭建过程整理给你。<!--more-->这篇文章适用于对maven有足够了解的读者，如果你还不认识maven，欢迎阅读我的另一篇文章：

> [一篇就够 \| 快速理解什么是maven](/onepostenough/2020/05/04/OPE-fast-know-maven/)

内容预览：
* 讨论什么是“框架”
* 展示一个简单的基于 maven 特性搭建的自制框架
* 展示上述自制框架的使用示例
* 自制框架的搭建过程

## 一、什么是框架

### 概念

笔者认为，所谓的框架，是指一套抽象的规范，符合某一框架的规范，则可称为使用了这一框架或者基于这一框架。

举个例子，maven项目要求在根路径有一个配置文件 pom.xml，还要求项目源代码、项目测试代码、项目静态资源必须放置到指定的目录里；再举个例子，Spring项目需要定义或配置各种bean，注册到容器里的bean，可以被依赖注入注解来管理使用，完成IoC；最后再举个例子，MybatisORM框架，一方面需要通过配置文件指代清楚Mapper代码类所在的位置，一方面要在配置好的静态文件目录里完成*Mapper.xml文件的内容。

框架有轻重之分，所谓轻量级的框架，是指使用框架与不使用框架的区别并不明显，框架规范对传统开发侵入性低；而重量级的框架则相反，框架规范对传统开发的侵入性高，使用框架与不使用框架的区别很明显。

## 二、自制框架 - zty-framework

### 作用概述

zty-framework 属于轻量级框架，完全基于 maven 项目框架的特性对 Spring 框架进行封装，为不同种类的开发项目提供与项目类型对应的整套 Spring 依赖，并且还定义了一套专有的规范。主要功能如下：

1. 简化 Spring 项目搭建过程。按功能类型封装常用功能依赖包，统一管理，对外提供完整的"依赖包套餐"。只需引入 zty-framework 的相应模块，即可完成对某一功能类型所需的所有依赖包的导入过程，既避免了重复引入依赖的人工操作，也大大减少修改依赖引入所需的工作量。
2. 定义规范，减少重复工作，提升开发效率，改善开发质量。针对绝大多数开发场景，zty-framework 抽象出了一套通用的参数规范、异常信息规范和注解规范。开发者遵从这些规范进行开发，可以很方便地完成统一参数校验、统一异常处理，既减轻了工作量，也改善了开发质量。

如果将 Spring 框架的各部分内容比喻成小积木的话，那么 zty-framework 的各部分内容则可以理解为——由几个小积木组建成的模块。

### 框架内容展示

首先是 zty-framework 的目录结构图：

![zty-framework 目录结构](https://s1.ax1x.com/2020/05/13/YwP5z8.png)

对于负责统一实现并管理实体类、通用类(公共类)、工具类的模块，zty-framework 抽象出了 framework-common，其他项目只需引入 framework-common 依赖，即可完成所需依赖包的导入。framework-common 的 maven 依赖图如下：

![framework-common 依赖图](https://s1.ax1x.com/2020/05/13/YwiSQU.png)

zty-framework 的规范类，在 framework-common 里面进行了实现。分别是这四部分：1）框架自定义注解；2）框架规范参数类；3）框架异常规范类；4）框架工具类。如果需修改这些内容，只需在 framework-common 里进行修改即可。

![framework-common 内容](https://s1.ax1x.com/2020/05/13/YwPxzT.png)

对于负责实现与数据库交互、完成业务功能的模块，zty-framework 抽象出了 framework-bo（BO表示Business Object，这里指业务对象层），其他项目只需引入 frame-bo 即完成了对所需依赖的导入。framework-bo 的 maven 依赖图如下：

![framework-bo 依赖图](https://s1.ax1x.com/2020/05/13/YwipyF.png)

对于负责对外提供API接口、接口参数处理的模块，zty-framework 抽象出了 framework-web，其他项目只需引入 frame-web 即完成了对所需依赖的导入。framework-web 的 maven 依赖图如下：

![framework-web 依赖图](https://s1.ax1x.com/2020/05/13/YwP7LQ.png)

对于按实际需要集成各模块、生成可部署项目的模块，zty-framework 抽象出了 framework-springboot-app 模块，maven 依赖图如下：

![framework-springboot-app 依赖图](https://s1.ax1x.com/2020/05/13/Ywi9L4.png)


以上只是笔者搭建的示例，framework 各模块的依赖可以按需选择、调整。

### 使用示例

以实际项目中“账号模块”的实现作为 zty-framework 的使用示例，带你更近一步感受 zty-framework 的便利。

首先是创建负责定义公用实体类的 account-common 模块，引入 framework-common 依赖：

![account-common 依赖图](https://s1.ax1x.com/2020/05/13/YwPqds.png)

account-common 的实体类包括数据对象类（DO）和数据传输对象类（DTO），其中DO表示数据库表结构相对应的实体类，DTO表示用于传输的字段脱敏后的类，POJO命名遵从[阿里巴巴开发规范](https://edu.aliyun.com/certification/cldt02)：

![account-common 内容](https://s1.ax1x.com/2020/05/13/YwPLon.png)

第二步是创建负责完成与数据库交互的 account-bo 模块，引入 framework-bo 和 account-common 依赖：

![account-bo 依赖图](https://s1.ax1x.com/2020/05/13/YwPoQS.png)

account-bo 模块的内容主要包括DAO类和Service类，如果业务涉及到复杂流程的实现，还可以基于Service类提供的方法，实现API类：

![account-bo 内容](https://s1.ax1x.com/2020/05/13/YwPbZj.png)

第三步是创建负责提供 http 接口的 account-web 模块，引入 framework-web 和 account-bo 依赖：

![account-web 依赖图](https://s1.ax1x.com/2020/05/13/YwPvWV.png)

account-web 主要实现 Controller 类，完成参数检查，调用 bo 层的接口方法实现功能：

![account-web 内容](https://s1.ax1x.com/2020/05/13/YwPXiq.png)

最后一步，结合实际需求，对各个功能模块进行集成，搭建一个可部署的项目。这里的 service-customer 模块引入了"账号管理模块"、"微信授权模块"、"文件管理模块"和"缓存管理模块"的依赖，当然还有 framework-springboot-app，完整依赖图如下：

![service-customer 依赖图](https://s1.ax1x.com/2020/05/13/YwPjJ0.png)

各个其他模块的功能，皆已在各模块内完成了实现，service-customer 只需基于 Spring AOP 按业务需求完成统一参数处理和统一异常处理即可：

![service-customer 内容](https://s1.ax1x.com/2020/05/13/YwPTsg.png)

### 搭建过程

1. 创建 maven 空工程，命名为 framework；
2. 将工程 framework 的 pom.xml 的 \<packaging\> 改为 `pom`;
3. 在工程 framework 的 pom.xml 里定义框架的子模块，声明到 \<modules\> 里；

前3步的pom.xml完整代码如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
          http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.4.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <!-- 定义基本信息 -->
    <artifactId>framework</artifactId>
    <groupId>com.zty</groupId>
    <version>${zty-framework.version}</version>

    <!-- 父模块必须设置为此 -->
    <packaging>pom</packaging>

    <!-- 集中版本管理 -->
    <properties>
        <zty-framework.version>0.1.1</zty-framework.version>
    </properties>

    <!-- 声明子模块 -->
    <modules>
        <module>framework-common</module>
        <module>framework-web</module>
        <module>framework-bo</module>
        <module>framework-springboot-app</module>
    </modules>
</project>
```

4. 分别创建框架子模块 framework-common、framework-bo、framework-web 和 framework-springboot-app，并在 \<parent\> 标签里使他们继承于 framework；
5. 在相应的模块里引入依赖；
6. 如果需要，实现相应模块的代码类；

framework-common 的 pom.xml：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
          http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>framework</artifactId>
        <groupId>com.zty</groupId>
        <!-- 继用父项目的版本 -->
        <version>${zty-framework.version}</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>framework-common</artifactId>
    <groupId>com.zty</groupId>
    <!-- 继用父项目的版本 -->
    <version>${zty-framework.version}</version>

    <dependencies>
        ...
    </dependencies>
</project>
```

___

### 结尾

好的，maven最佳实践——教你搭建自制的开发框架到此正式结束了。[《一篇就够》](/tagSort/one-post-enough/) 系列是我沉淀各种知识整理而成的文章，只有沉淀到足够教会一个完全新人的程度我才会在里面写文章，每一篇都是我倾尽当时的所有才华所写的精品文章，欢迎常来逛逛哦。

![我的微信二维码](https://s1.ax1x.com/2020/05/13/YwZ2X6.jpg)

我是一个自我定位为“喜欢开发有趣工具的Java开发者"，如果对我的文章有任何疑惑或者想交流的地方，欢迎添加我的微信，二维码如上。

 