---
layout: post
title:  "项目日记 | 日语50音消消乐"
date:   2018-08-27 18:50:50 +0800
categories: projectDiary
permalink: /:categories/:year/:month/:day/:title/
tags: 
- 微信小程序
- NodeJs后端
- 日语50音
- 消消乐
excerpt_separator: <!--more-->
---

如今的小程序开发如火如荼，而笔者接触过小程序开发后，认为小程序后端更适合用充血模型来写（PHP、node.js、Python等），而微信团队也为每个小程序开发者配备一个免费的专门部署该小程序后端项目的云服务器（仅支持PHP、node.js这两种单线程语言）。所以，为了更方便地开发小程序，笔者决定学习node.js，并仿照 *反义词消消乐* 小程序来开发一款面向0基础日语爱好者的产品——**日语50音消消乐**<!--more-->


现在是2018年8月25日（写于10:00 a.m. 刚摸索完微信公众号开发的权限）

>[本项目Github地址](https://github.com/imZTY/Japan50){:target="_blank"}

* 
{:toc}


## 文章内容预告
本文会按着日期把笔者的学习进度以及开发进度写进来，包括一些学习笔记以及开发细节




## 思维导图

![计划3日之内完成](https://upload-images.jianshu.io/upload_images/8463645-d8cabdc003ecb1ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)






## 一、node.js学习（8.25）


![学习材料](http://upload-images.jianshu.io/upload_images/8463645-cae27420c2cd3de5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


* **同步与异步体现JavaScript也颇具后端开发价值**（第四章）
同步的体现：回调函数、除了delay功能外的以分号分隔的每一句话
异步的体现：delay事件




* **Controller控制层的实现**（第五章、第十五章）
node.js可以通过下面的示例代码实现类似JavaWeb的Controller，实现业务的分发。其中，wx.request.get: https://bxee5pf9.qcloud.la//data `前面那个是小程序后端自动分配的https域名，后面会提到` 即可得到 json 格式的数据。做到这一步，就距离完成后端的搭建就只差node.js和mysql的交互了！！

```
// 引入包
var http = require('http'),
    url = require('url');


//定义测试对象
var obj = {
  name : "Officer",
  surname : "Dibble"
}
//相互转化
var json = JSON.stringify(obj);
var parsedJson = JSON.parse(json);


// 创建服务器
http.createServer(function (req, res) {
  var pathname = url.parse(req.url).pathname;

  if (pathname === '/') {   //默认首页（普通nodejs学习）
      res.writeHead(200, {
      'Content-Type': 'text/plain'
    });
    res.end('Home Page\n');
  } else if (pathname === '/about') {   //测试跳转页面（普通nodejs学习）
      res.writeHead(200, {
      'Content-Type': 'text/plain'
    });
    res.end('About Us\n');
  } else if (pathname === '/data') {   //小程序测试数据API（返回json数据）
  	  res.writeHead(200, {
      'Content-Type': 'text/plain'
    });
    res.end(json);
  } else {
      res.writeHead(404, {   //报错设置
      'Content-Type': 'text/plain'
    });
    res.end('Page not found\n');
  }
//小程序后端服务器默认开放5757端口
}).listen(5757, "127.0.0.1");
```



* **数据库表的设计**（存放笔记数据）
每一个小程序账号都可以免费开通一个无法进入终端的腾讯云服务器，详见[官方教程](https://cloud.tencent.com/document/product/619/11447){:target="_blank"}。开通后再重新建立一个 **node.js快速启动模板** 小程序项目，即可自动生成含有后端代码示例的项目，注释掉其中的核心代码，换上上一小节的代码就可以使用了。（PS：首次上传代码需要初始化服务器的配置，要耐心等上一点时间，完成后有惊喜）

```
CREATE TABLE `notes` (
  `id` int(11) NOT NULL COMMENT '主键',
  `title` varchar(15) NOT NULL COMMENT '笔记标题',
  `content` text NOT NULL COMMENT '内容',
  `author` varchar(10) NOT NULL COMMENT '署名',
  `create_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `password` varchar(15) DEFAULT NULL COMMENT '密码',
  `update_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  `star` int(4) NOT NULL DEFAULT '0' COMMENT '星星数'
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

ALTER TABLE `notes`
  ADD PRIMARY KEY (`id`);

ALTER TABLE `notes`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键';COMMIT;
```

*没想到配给小程序的服务器居然自带mysql（含GUI），而笔者接触最多的也是mysql，所以就不折腾MongoDB了*


* **node.js与mysql的交互**
到这里，笔者认为有必要顺便学一下node.js的封装方式，这样可以实现解耦，MVC分层的项目最容易修改逻辑了。目标：1.跨文件调用方法 2.跨文件返回数据。

(1)  跨文件调用方法
(module.exports >) [object].function

```
/* ========= 这里是   server.js  ======== */
var service=require('./MVC/service');
service.initModelList();
```

(2) 跨文件返回数据
module.exports = [object]

```
/* ========= 这里是     ./MVC/service  ======== */
//初始化
var initModelList = function(){
	//运行时的特效，可用于检验逻辑
	console.log("[Service function] initModelList");
	//循环补全数组
	for (var i = 0; i < 23; i++) {
		//假装在初始化
	}
}

//返回方法
module.exports = {
	checkPassword
}
```




*------------------------  8.26  ------------------------*

*学习新技术最好的方式是看[官方文档](https://www.npmjs.com/package/mysql#performing-queries){:target="_blank"}或看书，其次是搜[博客](https://www.cnblogs.com/wuxiang/p/4598178.html){:target="_blank"}。*
node.js 与 mysql 交互流程如下：
1. 创建连接

```
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host: 'localhost',
  port: 3306,
  user: 'root',
  database: 'japan',
  password: 'root',
  charset: 'utf8'
});

var startConnection = function(){
	//运行时的特效，可用于检验逻辑
	console.log("[DAO function] startConnection");
	connection.connect();
}

var closeConnection = function(){
	//运行时的特效，可用于检验逻辑
	console.log("[DAO function] closeConnection");
	connection.end();
}
```

2. 设计SQL语句并执行

```
var creadNote = function(note){
	//运行时的特效，可用于检验逻辑
	console.log("[DAO function] creadNote");
	connection.query(
	  'INSERT INTO notes ( title, content, author, password ) VALUES ( ?, ?, ?, ? )',
	  [note.title, note.content, note.author, note.password],
	  function (error, results, fields) {
	    // error will be an Error if one occurred during the query
	    // results will contain the results of the query
	    // fields will contain information about the returned results fields (if any)
	    if (error) throw error;
	    return results;
	  }
	);
}
```

3. 几个瓶颈
（1）JS的深拷贝和浅拷贝
（2）node.js 返回时，要将对象转化为json数据，否则会报错，注意，若没有报错而是返回空值，则是其他问题（返回的对象为空值）
（3）node.js 中的 mysql 做查询时，要不停地 callback 直到返回给用户，否则将返回空值

```
var getList = function(callback){
	//运行时的特效，可用于检验逻辑
	console.log("[DAO function] getList");
	connection.query(
	  'SELECT * FROM `notes`',
	  function (error, results, fields) {
	    // error will be an Error if one occurred during the query
	    // results will contain the results of the query
	    // fields will contain information about the returned results fields (if any)
	    if (error) throw error;
	    result=JSON.stringify(results);
	    callback(result);
	  }
	);
}
```


*好了，有了这些基础知识，后端就可以搭建完了*
![接口备忘表](https://upload-images.jianshu.io/upload_images/8463645-0907a28047e17d50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)








* **日文50音的获取**
1. 从[百度百科](https://baike.baidu.com/link?url=Kyk2qY-KM6PeNNsyPhHz6xk1FamPoEGPkf2JUvTNzwO1CxSNMaEvSX5IAUIqWLSUBIUh9GBJWEbsgUq7u-TCq_sXy_emT0UZs6qYXbRLF6W#5_4){:target="_blank"}获取所有文字数据
![处理结果](https://upload-images.jianshu.io/upload_images/8463645-5e56a6f3dae7202e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 解读百度语音api
解读后发现[百度语音合成](http://ai.baidu.com/docs#/TTS-API/41ac79a6){:target="_blank"}不支持日文。而且这种自动合成的服务（[科大讯飞](https://doc.xfyun.cn/rest_api/%E8%AF%AD%E9%9F%B3%E5%90%88%E6%88%90.html){:target="_blank"}依然），声音也[一般般](http://fanyi.baidu.com/translate?aldtype=16047&query=&keyfrom=baidu&smartresult=dict&lang=auto2zh#jp/zh/%E3%81%82%0A%E3%81%8B%0A%E3%81%95%0A%E3%81%9F%0A%E3%81%AA%0A%E3%81%AF%0A%E3%81%BE%0A%E3%82%84%0A%E3%82%89%0A%E3%82%8F%0A%E3%82%93%0A%E3%81%8C%0A%E3%81%96%0A%E3%81%A0%0A%E3%81%B0%0A%E3%81%B1%0A%E3%81%84%0A%E3%81%8D%0A%E3%81%97){:target="_blank"}。或许这种情况下更适合用[真人录音](http://o-oo.net.cn/50yinmp3/){:target="_blank"}吧。

3. 为了便于整理，还是把音频文件爬下来吧

```
import requests
import csv,codecs
from pyquery import PyQuery as pq

rooturl='http://o-oo.net.cn/50yinmp3/'

def do():
    # 新建文件存储数据
    with codecs.open('japan50.csv', 'w','utf_8_sig') as csvf:
        fieldnames=['No','Hiragana', 'url']
        writer=csv.DictWriter(csvf,fieldnames=fieldnames)
        writer.writeheader()
        csvf.close()
    # 访问小楠日语50音页面
    response=requests.get(rooturl)
    # 预处理，除去无关url
    doc=pq(response.content).remove_namespaces()
    table=doc('.table-striped')
    items=table.find('td').items()
    i=1
    h='あ'
    with codecs.open('japan50.csv', 'a+','utf_8_sig') as csvf:
        fieldnames=['No','Hiragana', 'url']
        writer=csv.DictWriter(csvf,fieldnames=fieldnames)
        for item in items:
            if(i%2!=0):
                h=item.text()
            else:
                message={
                    'No':i/2,
                    'Hiragana':h,
                    'url':item('audio').attr('src')
                }
                print(message)
                writer.writerow(message)
            i=i+1
        csvf.close()     
   
do()
```

![处理结果](https://upload-images.jianshu.io/upload_images/8463645-6ac851c9b16921df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


4. 按一定规则上传到小程序CDN
再次使用快速编程手枪——Python3进行数据处理

```
import urllib.request as req
import xlrd

h='./mp3/h/'
k='./mp3/k/'

def do():
    workbook1=xlrd.open_workbook(r'japan50.xlsx')
    sheets1 = workbook1.sheet_names()
    print("wordSHEET= ",sheets1[2])
    wordSHEET = workbook1.sheet_by_name(sheets1[2])
    print(wordSHEET.nrows-1)
    for a in range(1,wordSHEET.nrows):
        ROW=wordSHEET.row_values(a)
        #Hiragana
        req.urlretrieve(ROW[2],h+ROW[0]+'.mp3')
        #Katakana
        req.urlretrieve(ROW[2],k+ROW[1]+'.mp3')
        
do()
```

![处理结果](https://upload-images.jianshu.io/upload_images/8463645-80d6c471a2114ecd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![上传到小程序平台的CDN](https://upload-images.jianshu.io/upload_images/8463645-ebb3013ba24bde70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





*------------------------  8.27  ------------------------*
*今天的时间都用来实现页面了，到晚上提交审核了才有时间写博*

## 二、游戏页面实现
*这里算是整个项目中最考验智慧的地方了，这个时候不应该鲁莽地死磕，而应梳理好合适的思路再行动，避免做无用功。*
1. **和传统消消乐的对比**
普通的消消乐：棋盘格子多、消除子种类少且不限制每种消除子同时出现的个数。
50音消消乐：棋盘格子少、消除子种类多且限制每对消除子必须同时出现。
2. **棋盘刷新业务归纳**
（1）平假名和片假名以罗马音配对，没一对必须同时出现在棋盘上
（2）消除子随机出现在盘上，确保游戏的公正无规律性
3. **棋盘刷新思路与算法**
* 思路：
（1）双进程同步刷新消除子，实现消除子的成对性
（2）每个格子生成[随机数](https://www.cnblogs.com/starof/p/4988516.html){:target="_blank"}，完成后再按随机数对格子排序，实现刷新的无规律性
（3）顺序遍历所有棋盘格，以有序的方法实现无序，提升算法效率（起码不用随机生成坐标后再判断该格子是否可落子）
* 算法：*（啰啰嗦嗦暴力算法写了近100行）*

```
 /** 
   * 备注：
   * 1. 棋盘大小 4×4
   * 2. 100000000是为了尽量减小随机数 rand[] 出现相同的情况 (否则将报错)
   */
  refresh:function(){
    //判断取大取小（以排序后的左端为选取文字的标准还是以右端）Z[0, 1]
    var judge = new Array(8);
    for (var i = 0; i < judge.length; i++) {
      judge[i] = Math.round(Math.random());
    }
    //对应每个格子的随机数 Z[0, 99]
    var rand = new Array(16);
    for (var i = 0; i < rand.length; i++) {
      rand[i] = Math.floor(Math.random()*100000000);
    }
    //rand[]数组每个格子对应的排序序号（升序序号）
    var sort = new Array(16);
    var n = 1;
    for (var i = 0; i < sort.length; i++) {
      n = 1; 
      for (var j = 0; j < rand.length; j++) {
        if (rand[i] > rand[j]) {
          n++;
        }else{
          continue;
        }
      }
      sort[i] = n;
    }
    //合并 sort 和 rand
    var connect = new Array(16);
    for (var i = 0; i < connect.length; i++) {
      connect[i]={
        rand:rand[i],
        sort:sort[i]
      };
    }
    //存放排序后的 rand
    var sortedRandom = new Array(16);
    for (var j = 1; j < 17; j++) {
      //按照 sort 对 rand 排序
      for (var i = 0; i < sortedRandom.length; i++) {
        if (sort[i]==j) {
          sortedRandom[j-1]=rand[i];
        }else{
          continue;
        }
      }
    }
    
    //刷新业务
    var that=this;
    var L = that.data.hiragana.length;
    
    for (var i = 0; i < connect.length; i++) { //i遍历所有格子
      var x = Math.floor(i/4);
      var y = i - x*4;
      var value = connect[i].sort;//当前格子的随机排序值
      var no = 'chess['+x+']['+y+'].no';
      var word = 'chess['+x+']['+y+'].word';
      var url = 'chess['+x+']['+y+'].url';

      if (value < 9) { //分开 sort[1, 8] sort[9, 16] （输入类型 大/小） 输入=小
        //随机大小标准
        if (judge[value-1]==0) {//无需折半获取判断值     （输出结果  取大还是取小  输入是否有效）
          that.setData({
            [no]:value,
            [word]:that.data.hiragana[Math.floor(connect[i].rand*L/100000000)].word,
            [url]:that.data.hiragana[Math.floor(connect[i].rand*L/100000000)].voice
          });
        }else{ //以大为准，则此处跳过             （大之处理）
          that.setData({
            [no]:value,
            [word]:that.data.katakana[Math.floor(sortedRandom[16-value]*L/100000000)].word,
            [url]:that.data.katakana[Math.floor(sortedRandom[16-value]*L/100000000)].voice
          });
        }
      }else{                                      //     输入=大
        if (judge[16-value]==0) {//需镜返获取判断值     （输出结果  取大还是取小  输入是否有效）（小之处理）value]*L/100000000)].word);
          that.setData({
            [no]:value,
            [word]:that.data.katakana[Math.floor(sortedRandom[16-value]*L/100000000)].word,
            [url]:that.data.katakana[Math.floor(sortedRandom[16-value]*L/100000000)].voice
          });
        }else{ //以大为准，则此处执行
          that.setData({
            [no]:value,
            [word]:that.data.hiragana[Math.floor(connect[i].rand*L/100000000)].word,
            [url]:that.data.hiragana[Math.floor(connect[i].rand*L/100000000)].voice
          });
        }
      }
    }
  },
```
![游戏页面(含发音)](https://upload-images.jianshu.io/upload_images/8463645-c896adc02000f010.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 三、笔记页面实现
既然后端搭建好了，这里难度不大，主要工作包括：1.布局实现 2.数据渲染
[边框干货](https://blog.csdn.net/qq_32067045/article/details/53939351){:target="_blank"}
![笔记页面](https://upload-images.jianshu.io/upload_images/8463645-01d8522e83ca0ced.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 四、要点总结
*写了一天前端，先从前端开始说吧，总结一下本次项目中一些发挥了重要作用的东西*
* **前端方面**：
（1）要注意this.setData({ })的各种用法，尤其是数组对象的拼接，因为之前踩过坑，积累下来的经验使我这次前端开发整体顺利。
```
var that=this;
......
 var no = 'chess['+x+']['+y+'].no';
 var word = 'chess['+x+']['+y+'].word';
 var url = 'chess['+x+']['+y+'].url';
......
that.setData({
      [no]:value,
      [word]:that.data.hiragana[Math.floor(connect[i].rand*L/100000000)].word,
      [url]:that.data.hiragana[Math.floor(connect[i].rand*L/100000000)].voice
  });
```
（2）[wx:for](https://www.w3cschool.cn/weixinapp/weixinapp-list.html){:target="_blank"}实现循环渲染，[wx:if](https://www.w3cschool.cn/weixinapp/weixinapp-conditional.html){:target="_blank"}实现条件渲染，这两个是实现动态渲染以及游戏逻辑的重要工具
（3）[WXSS](https://www.w3cschool.cn/weixinapp/weixinapp-wxss.html){:target="_blank"}的积累，例如padding、margin等css样式，规律是：上 右 下 左 （或：上下 左右），还有 flex 很实用布局的样式设置也很实用

*如果一个产品代表着一个武侠的话，上面三个点则方别代表着：内功(数据的流转)、武功(数据的加载)、武器(用户交互界面)*
* **后端方面**：
（1）在分层思想的基础上开发很重要，可以使思路清晰，代码也容易找到与修改
（2）对后端的作用有较深后，使用不同语言进行后端开发其实是差不多的，无非就是 业务的分发(Controller、DTO)+业务的实现(Service、DAO) 罢了


## 五、展望未来
更新方向：
1. 完善游戏逻辑（添加游戏说明）
2. 实现添加与修改笔记功能（为了满足用户一个人使用的需求）
3. 实现笔记列表的下拉加载、实现笔记的按作者查询（为了方便用户以作笔记的形式与日语学习者交流，分享干货，共同积累）
4. 实现笔记点赞功能（增强本产品的平台性，提升价值与趣味）

![日语50音消消乐](https://upload-images.jianshu.io/upload_images/8463645-c305028487c575e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


___
感想：
1.如果贫血模型springboot（Java）是自动步枪的话，那么充血模型node.js就是自动手枪，像小程序这种小项目，用手枪就够了。两者同样是为了命中目标而被设计出来的工具罢了，理解了射击的原理，学习枪支的使用还是蛮简单的。
2.前端实现的效率还是低，没能按计划完成所有页面，前端也是一个需要经验积累的领域，有经验则方便（数据传递与渲染），无经验则难行（WXSS样式）。
3.第一次以写博客日记的形式记录做项目的过程，感觉效率不错，一方面督促自己提高效率，另一方便锻炼自己的表达能力，满满的健康感。
4.不过可惜但只好接受的是，理想的功能并未完全实现，仅仅达到基本能用的程度（自我评价65分吧），要开学了，以后有时间再完善之。（如果后面觉得项目达到值得传到开源社区的级别，我再把链接发上来）

___
*本人总结的学习新技能步骤：
1.hello world尝试，明白基本理论（明白了理论就具备了解读优秀作品的能力）
2.解读优秀作品（例如借鉴先导们的作品，结合自身的实际需求进行修改，投入到实际的使用中，在使用中消化知识、感悟知识）
3.自己从0开始独立开发一次，通过实践成为别人的先导，巩固这项新技能。*
>学习知识 = 进食 + 咀嚼 + 消化 + 吸收<br>
>进食 = 阅读/学习，掌握基本理论、掌握赏析能力<br>
>咀嚼 = 做笔记整理/解读优秀作品（顺便再次阅读/学习）<br>
>消化 = 反复思考+理解<br>
>吸收 = 在实际生活学习或项目中尝试使用该知识、感受该知识<br>
[——《如何高效学习》](https://book.douban.com/subject/25783654/){:target="_blank"}
 




*------------------------  后续  8.28  ------------------------*

[小程序计时器](https://www.cnblogs.com/i-douya/p/8807454.html)
[小程序自定义弹窗](https://blog.csdn.net/zhuyb829/article/details/73349295)
[小程序<input>数据的获取](https://developers.weixin.qq.com/miniprogram/dev/component/input.html)
[小程序<text>省略超长内容](https://www.jianshu.com/p/3b70710c7633)
[小程序动态改变页面标题](https://developers.weixin.qq.com/miniprogram/dev/api/ui.html)
[小程序字体样式小结](https://blog.csdn.net/qq_32067045/article/details/53943739)
[小程序布局小结](https://blog.csdn.net/aoaoxiexie/article/details/53991432)
 

*------------------------  后续  8.29  ------------------------*

管窥带来的带宽减少效应越来越明显了，今天之内一定要把 “三天计划” 想达到的程度实现！

2018.8.29  11:35  a.m. 基本实现 “三天计划” 想达到的程度，达到自评90分的程度并提交审核。

2018.8.31  14:22  p.m. 修改三次，通过审核（只剩下游戏页面）

![审核历程](https://upload-images.jianshu.io/upload_images/8463645-4073d3e3ad461026.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![游戏页面做得还可以 25分](https://upload-images.jianshu.io/upload_images/8463645-1e6ac92576e01c4a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![笔记列表页也还行 24分](https://upload-images.jianshu.io/upload_images/8463645-22e0d56c3b63e7c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![笔记详情页 23分](https://upload-images.jianshu.io/upload_images/8463645-0059de00b588037f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![编辑笔记页功能齐全但丑 18分](https://upload-images.jianshu.io/upload_images/8463645-6932790ada8b1be5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

