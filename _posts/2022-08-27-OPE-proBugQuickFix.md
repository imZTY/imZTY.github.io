---
layout: post
title:  "一篇就够 | 定位生产问题CheckList"
date:   2022-08-25 22:56:10 +0800
categories: onePostEnough
permalink: /:categories/:year/:month/:day/:title/
tags: 
- 高效定位问题
- CheckList
- 系统优化
excerpt_separator: <!--more-->
---

由一次生产问题延伸出来的知识沉淀。当业务发展到了网络带宽跑满的时候，会发生这种事情。<!--more-->

-  
{:toc}

### 背景描述：

我司是主要给银行做收单系统的，其中有一家银行对资源利用率的追求比较高(抠抠搜搜)，这家银行给我们提供的CPU、内存、磁盘、网络带宽、数据库连接数都很有限，2C服务的平均资源使用率达到80%以上，非常饱和。我们系统的跟其他业务系统共用一个公网IP，相当于共用这个IP的网络带宽。

随着银行业务发展扩展，系统要处理的数据量和请求量越来越大，直到有一天，业务高峰期网络带宽跑满了，发生了因为网络带宽不足引起数据包丢失，最终导致系统核心功能偶尔不可用的生产事故（聚合支付H5打不不开）。


### 关键过程简述：

1. 客服同事向客户索要问题复现的视频录像：客户扫描我们的聚合码 打不开，扫描支付宝原生付款码可以打开
2. 从录像里得到具体二维码，转化为具体的url，前端访问 尝试复现问题，发现有几个静态资源响应失败
3. 去Nginx日志里 通过请求时间 找出现异常的url，发现没记录
4. 在前端机器 ping 异常url的域名，发现偶尔会出现丢包的情况
5. 使用 curl 制作定时任务获取接口耗时详细数据（路由时间、建立连接时间、开始传输时间、总时间等）
6. 具体优化措施：(1)nginx调大gzip压缩率，对超过1k的文件进行压缩；(2)关闭管理平台部分功能，在高峰期禁用，优先保证核心功能有足够的网络带宽；(3)梳理生产机器网络访问链路，**将公网访问地址调整为内网访问地址**；
7. 再次使用 curl 制作定时任务获取接口耗时详细数据（路由时间、建立连接时间、开始传输时间、总时间等），与步骤5的数据进行对比，优化结果：(1)高峰期接口最高耗时缩短了60%，6.5s --> 3.0s；(2)高峰期接口平均耗时缩短了0.01s，0.04s --> 0.03s；


### 问题定位CheckList：

|检查方向 | 关键指标 | 快速确认CheckList | 长久优化方向| 相关资料|
|:--|:--|:--|:--|:--|
|用户网络 | 是否能流畅上网 | 让用户提供问题复现的资料(如:视频、请求记录等)，目的是为了获取更多的客观信息(请求地址、请求时间、请求报文、响应报文、耗时等) | 1. 前端指标监控告警<br/>2. 前端指标优化(LCP、FID、CLS) | [Sentry前端监控库](https://docs.sentry.io/){:target="_blank"} |
|服务器网络 | 带宽饱和度、LB是否正常、有无丢包 | 1. 先去网络流量监控平台或者咨询网络运维同事，检查带宽饱和度<br/>2. 去分析LB工具的日志(如Nginx)，分析负载均衡是正常，能否将请求正确地转发到服务器<br/>3. 在前端机器 ping 服务器，持续观察 看有无丢包发生 丢包频率有多高 | 1. 网络带宽指标监控告警<br>2. 静态资源文件开启nginx gzip压缩(html、js、css、json)<br/>3. 图片资源类型转换(png支持无损压缩文件大，jpg不支持无损压缩文件小)<br/>4. 梳理生产环境服务访问链路，将走公网的链路改为走内网访问 | [curl打印连接详细信息](https://blog.josephscott.org/2011/10/14/timing-details-with-curl/){:target="_blank"} |
|机器资源 | CPU、MEM、IO | 1. 如果没有机器资源监控平台，则进入生产机器 top 查看实时机器资源使用情况 | 1. 机器资源指标监控告警<br/>2. 机器资源扩容 | -|
|应用bug | ERROR日志 | 1. 如有ELK平台则进入ELK平台，没有则进入生产机器控制台<br/>2. 观察是否有异常日志`grep 'ERROR' application.log | wc -l` <br/>3. 观察异常业务日志的时间间隔，分析处理时间是否正常 | 1. 关键业务异常加告警<br/>2. 分级管理应用，优先确保核心应用的高可用<br/>3. 丰富配置项，使用配置来控制关键的参数(如:连接数大小、线程数大小等)，以便遇到问题时能有更多的临时解决方案(例如扩容)<br/>4. 关键逻辑节点多打日志，用磁盘空间换取定位解决问题的时间 | - |
|数据库 | CPU、内存 | 1. 联系DBA同事 确认数据库是否运作正常<br/>2. 连接数据库，执行sql验证确认 | 1. 数据库指标加告警<br/>2. 慢sql优化，尽量走索引<br/>3. 数据库表结构优化(加索引/加分区) | - |
|第三方系统 | 网络、功能 | 1. 2. curl -I '第三方关键接口'<br/>2. 检查结果是否符合预期 | 1. 请求第三方指标监控告警<br/>2. 配置网络代理，提升网络通信速度 | - |

### 常用脚本：

1. 取值 去重 排序：`zgrep -a 'currentSmid:' application.2021-12-29.log.* | sed 's/^.*currentSmid:\s*\([0-9]\+\).*$/\1/' | sort | uniq -c`
2. 时间段日志统计：`zgrep '\"businessCode\":\"1010\"' application-2020-08-08.*.log.gz | awk -F '[|]' '{print $1}' |awk -F '[:]' '{print $2}' | uniq -c |more`
3. 指定日志指标排序：TODO
4. curl详细版：`curl [地址]`


### 系统监控：

经过对这次问题的复盘梳理，延伸出了一些对系统监控需要关注的点的理解。监控的两大目标 —— 1.问题发生的时候支持全链路追踪，高效解决问题；2.问题发生之前提前预知问题。


#### 前端监控最好这样做

1. 能监控到主流性能指标：LCP(最大可视区域渲染时间)、FID(首次加载延迟)、CLS(不稳定布局偏移评分)
2. 能上报错误信息
3. 能分级上报日志（开发时需增强 日志可读性 和 分级规范）
4. 能上报异常的请求信息（地址、时间、头、请求报文、响应报文）

#### 网络带宽监控最好这样做

1. 支持监控网络总带宽的使用百分比

#### Nginx监控最好这样做

1. 有统计指标指标折线图
2. 支持按时间切片统计各指标柱状图：请求次数、总流量、平均流量、平均耗时
3. 支持在指定时间段内，按指标对请求进行排序，找出最高/最低的N条记录
4. 能支持今天与昨天、最近7天、最近1个月的数据进行比较

#### 第三方接口监控最好这样做

1. 请求次数作为监控指标
2. 请求耗时作为监控指标
3. 业务响应是否成功作为监控指标


<style>
strong {
    color: red;
}
table th:first-of-type {
    width: 8vw;
}
table th:nth-of-type(2) {
    width: 12vw;
}
table th:nth-of-type(3) {
    width: 35vw;
}
table th:nth-of-type(4) {
    width: 35vw;
}
table th:nth-of-type(5) {
    width: 10vw;
}
</style>

