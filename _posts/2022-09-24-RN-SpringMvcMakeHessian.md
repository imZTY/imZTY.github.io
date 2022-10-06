---
layout: post
title:  "阅读笔记 | 基于SpingMVC实现Hessian通信协议"
date:   2022-09-24 09:02:26 +0800
categories: readingNote
permalink: /:categories/:year/:month/:day/:title/
tags: 
- 通信协议
- SpingMVC
- Hessian
- Armeria
excerpt_separator: <!--more-->
---

如何实现一个通信协议？这篇文章用SpingMVC告诉你。<!--more-->


* 
{:toc}

## 一、名词介绍

* hessian: 一个基于http的通信协议，服务端使用Servlet暴露接口

* armeria：是一个非常灵活的拓展性非常好的开源异步通信框架（[https://armeria.dev/](https://armeria.dev/){:target="_blank"}），它的愿景是能够支持所有微服务通信协议，目前支持：gRPC、Thrift、http1和2，服务注册与发现支持Eureka。（原生armeria是暂时不支持hessian协议的，需要自己实现拓展逻辑）

* armeria-eureka：是 Armeria 实现与 eureka 通信的模块（[https://mvnrepository.com/artifact/com.linecorp.armeria/armeria-eureka](https://mvnrepository.com/artifact/com.linecorp.armeria/armeria-eureka){:target="_blank"}），主要实现了 服务注册 与 服务发现 相关的能力。

* @HessianService：是一个自定义注解，在Bean类上使用它，无需额外配置，可以使这个Bean通过自定义的逻辑对外暴露Hessian服务提供者接口(暴露的地址可以配)。

* HessianClient：是一个自定义的类，其内容是使用Armeria客户端实现远程调用逻辑 —— 即 发送请求 与 处理响应

* @HessianClient：是一个自定义注解，在Bean的成员变量上使用它，可以通过SpringIoC机制将自定义的HessianClient对象引入(需要声明服务提供者地址)，这个Armeria客户端可以远程调用Hessian服务提供者的接口。（成员变量的类需要是Hessian服务提供者的同一个类）

## 二、核心实现逻辑

* @HessianService 功能实现原理：AnnotationHessianServiceResolver从springcontext获取带此注解的bean，得到BeanInfo，然后HessianExporterFactory使用BeanInfo创建HessianServiceExporter（声明接口与实现类），最后 HessianServiceHandlerMapping结合配置信息hessianProperties拼装hessianUrl并注册到springmvc里（默认url拼接方案 = /services/interfaceName.hs）

![@HessianService功能实现原理](https://i.v2ex.co/V37vP65Q.png)

* @HessianClient 功能实现原理：先使用SpringBootAutoConfigure基于启动配置注册EndpointBuilder，在基于已注册的有优先级的复合物EndpointBuilder创建HessianClientBeanFactory和HessianClientBeanPostProcessor，然后当需要向加了@HessianClient注解的地方注入BEAN对象时，HessianClientBeanPostProcessor调用HessianClientBeanFactory的create方法使用build模式创建HessianClient实例或代理实例（基于armeria框架的底层逻辑创建RpcClient，添加指标健康修饰器或日志修饰器），最后在Spring框架的IoC机制下将ArmeriaClient实例注入

```Java
/**
 * 具体代码实现思路，可以参考各支持SpringIoC的开源框架相关源码，如：
 * 1. SpringIoC原生通用实现 {@link org.springframework.context.annotation.CommonAnnotationBeanPostProcessor#postProcessProperties(org.springframework.beans.PropertyValues, java.lang.Object, java.lang.String)}
 * 2. Armeria重写的SpringIoC实现 {@link com.linecorp.armeria.spring.ArmeriaBeanPostProcessor#postProcessProperties(org.springframework.beans.PropertyValues, java.lang.Object, java.lang.String)}
 */
```

![@HessianClient功能实现原理](https://i.v2ex.co/WR81UK5I.png)

* 自定义ArmeriaClient实现hessian协议通信的逻辑：在Armeria框架的基础上，通过自定义的InvocationHandler实现 协议获取逻辑、连接信息获取与建立逻辑、请求数据流生成逻辑、响应数据流获取与解析逻辑。通过 通信协议+连接信息拼装完整的服务提供者url --> 建立连接 --> 将参数转换成Hessian协议的原生OutputStream并发送给服务端 --> 获取响应结果流并使用Hessian协议的原生InputStream进行解析 --> 解析后得到响应结果数据




## 三、延伸思考

### 3.1 完成一次RPC调度需要做哪些事情？

1. RPC客户端获取IP地址和端口：可以从配置获取，也可以从注册中心获取
2. RPC客户端与IP地址和端口建立连接：一般是TCP连接，http协议也是TCP连接
3. RPC客户端将信息通过已建立连接的输出流将信息输出给RPC服务端，并监听输入流等待服务端输入结果响应，与RPC相关的信息有：类坐标信息、方法坐标信息、参数数据、响应信息
4. RPC服务端从已建立连接的输入流里解析来自RPC客户端的信息，使用RPC客户端传来的数据调用具体方法，完成处理，最后将想要结果通过已建立连接的输出流将信息输出回给RPC客户端

### 3.2 一个RPC通信协议需要做哪些事情？

1. 定义清晰具体的报文格式规范，信息内容需包含：类坐标信息、方法坐标信息、参数数据。
2. 客户端统一按照这个报文规范传输流信息给服务端，并按照报文格式规范解析响应数据得到响应结果。
3. 服务端从流信息里按照报文格式规范解析出RPC信息，完成处理后将响应数据返回给客户端。

### 3.3 基于Armeria实现服务网格控制面，要怎么做？

1. 首先，不应该在ArmeriaClient端来实现服务网格控制面的逻辑。因为软件设计的"单一职责原则"告诉我们，客户端只应该负责建立连接并传输信息，服务网格控制面逻辑适合在"将连接信息提供给客户端"的地方来实现，例如注册中心，或者有能力影响注册中心返回连接信息给客户端的模块。
2. 如果非要在ArmeriaClient端来实现服务网格控制面的逻辑，则需要在获取连接信息后，判断一下这个信息是否满足使用条件，如果不健康需要更换满足使用条件的连接或抛出异常。


