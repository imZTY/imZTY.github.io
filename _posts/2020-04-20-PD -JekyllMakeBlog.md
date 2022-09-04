---
layout: post
title:  "项目日记 | Jekyll+GithubPage个人博客搭建过程"
date:   2020-04-20 20:20:50 +0800
categories: projectDiary
permalink: /:categories/:year/:month/:day/:title/
tags: 
- Jekyll
- Github Page
- 个人博客
excerpt_separator: <!--more-->
---

时间沙河滚滚前流，几年时间不过是千古之一瞬，2020届学生即将毕业。在即将毕业余闲充裕之际，我决定搭建一个 Github Page 个人博客，并作此文将重要步骤记录下来。<!--more-->鉴于此时在网上找到的文章皆认为未够细致，此文希望能够更详细全面地将 Github Page 个人博客的搭建过程展示给大家。如果你跟着我做，你也能做到同样的效果。

* 
{:toc}


----------------2020/04/17----------------

## 一、创建最简单的 Github Page

为什么要在 Github Page 搭建个人博客呢？总结优势有这几点：
* 可免去自己购买或搭建服务器的治理成本；
* 官方UI模板顺滑优雅，页面布局与样式完全支持自定义；
* 发布更新简单，将改动 push 到仓库即可完成，非常方便；
* Github Page除了适合用来搭建个人博客，还适合用于发布产品的官方文档，[这些大型开源工具](https://github.com/collections/github-pages-examples) 都是选择用 Github Page 作为文档说明站的，熟悉 Github Page 对以后制作开源项目说明文档会有帮助；

缺点：
* 没有评论、点赞系统，只支持静态资源；
* 无法调用网络API；

> 相关教程：<br>
>[利用 GitHub Pages 快速搭建个人博客](https://www.jianshu.com/p/e68fba58f75c)<br>
>[GitHub Pages 搭建教程](https://sspai.com/post/54608)<br>
>[三分钟在GitHub上搭建个人博客](https://zhuanlan.zhihu.com/p/28321740)<br>
>[搭建个人博客-hexo+github详细完整步骤](https://www.jianshu.com/p/189fd945f38f)

类似的文章还有很多，这些文章写得不错，帮到了很多人，但这些不能满足我本人的需求，这些文章很多要么只是写到搭建完 helloworld 级别的 Github Page 就没了，要么就是套用了开源博客模板。如果只是知道这些对以后的日常使用也会带来不便，因为有很多细节是自己不知道到的。例如当发现有某处不喜欢、想要修改，则需要看懂一个网络上的陌生人的项目代码再修改，想要对布局进行大调整则更是如此。因此，我打算自己学习相关语言的语法（主流的语言有 Jekyll、Hexo，本文选用 Github 推荐的 Jekyll），从0开始自己设计自己的布局，希望能像 [@你假笨](http://lovestblog.cn/about/index.html) 那样基于 Github Page 搭建自己设计的个人博客。

[GitHub Pages](https://pages.github.com/) 官网的最佳实践步骤如下：
1. 创建公共仓库，并按格式 `username.github.io` 给仓库命名：

![步骤1 - 创建仓库](https://upload-images.jianshu.io/upload_images/8463645-8d90b150c3b0bae4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 使用 git 将仓库克隆到本地：

![步骤2 - 使用命令行克隆](https://upload-images.jianshu.io/upload_images/8463645-1aed093b5d1c6552.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 创建 index.html 文件，并写入任意内容（可以是HTML也可以是其他内容）：

![步骤3 - 写入任意内容](https://upload-images.jianshu.io/upload_images/8463645-a3432aa795f0a726.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![步骤3 - 写入HTML](https://upload-images.jianshu.io/upload_images/8463645-68cef2d3d0b96592.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
4. 使用 git 提交改动到仓库（必须提交到 master 分支）：

![步骤4 - 提交代码](https://upload-images.jianshu.io/upload_images/8463645-3ac13706c0af95bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 访问`https://username.github.io`，查看结果：

![步骤5 - helloworld字符串结果](https://upload-images.jianshu.io/upload_images/8463645-d0eba474cc072e3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![步骤5 - 自定义HTML结果](https://upload-images.jianshu.io/upload_images/8463645-11c59ff51544e082.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样，算是完成了最简单的 hello world 实践，如果你想使用
Github官方提供的博客样式（基于Jekyll），可以这样做：
1. 进入仓库，在仓库页面选择进入setting模块：

![进入setting](https://upload-images.jianshu.io/upload_images/8463645-e16065be721cb29d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 在默认的 Option 栏目里，下拉直至 Github Page，进入并选择你喜欢的样式主题：

![Option栏](https://upload-images.jianshu.io/upload_images/8463645-76ef30bb45c25729.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![入口](https://upload-images.jianshu.io/upload_images/8463645-4e1b7e0268eb2394.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![选择你喜欢的主题](https://upload-images.jianshu.io/upload_images/8463645-ad5970d7a7c632b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 关于首页的说明：

Github Page 优先读取名为 index 的文件，其次再读取名为 README 的文件。例如有 index.html（或者 index.md），将则只会显示 index 的内容，：

无 index 且无 README，则会进入404提示页：

![404](https://upload-images.jianshu.io/upload_images/8463645-5d2ed5721ec69f94.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

有 index 或 README 的效果：

![正常](https://upload-images.jianshu.io/upload_images/8463645-425456eb6378dc78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到这里，hello world 实践算是正式完成了。

## 二、学习 Jekyll 对 Github Page 进行细节调整

经过上面的 hello world 实践，我们基本可以猜到 Jekyll 是一款作用于 markdown 排版样式的语言/工具，到底是不是这样呢，[Github Page文档](https://help.github.com/en/github/working-with-github-pages) 有这些相关说明：

![文档内容](https://upload-images.jianshu.io/upload_images/8463645-286dc16a522ad903.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

阅读完后发现，这些文章是站在 Github Page 的角度描述如何使用 Jekyll 的，想要更好地学会 Jekyll 还是要看 [Jekyll 官方文档](https://jekyllrb.com/docs/)。今天阅读完官方文档的说明并实践，总结的内容如下：

### 安装 Jekyll 的运行环境


第一步：安装 Ruby 与 RubyGems
打开 [windows端Ruby官方安装包下载地址](https://rubyinstaller.org/downloads/)，选择 WITH DEVKIT 栏目下推荐版本（已包含RubyGems），下载-安装-环境配置 完成后，通过指令`gem -v`检验是否成功

第二步：使用 Ruby 的 gem 指令安装 Jekyll
`gem install jekyll bundler`

第三步：检验是否成功
`jekyll -v`

第四步：创建你的第一个 Jekyll 工程
```shell
> jekyll new ./jekyllLearn          # 创建工程 
> cd myblog                         # 进入目录
> bundle exec jekyll serve          # 启动项目
> start http://localhost:4000       # 浏览器访问
> jekyll build --safe jekyll        # 代码提交前，检查打包情况，以便快速更新
```

### Jekyll 项目的目录结构

>[官方结构树]([https://jekyllrb.com/docs/structure/](https://jekyllrb.com/docs/structure/)
)：<br>
.<br>
├── _config.yml<br>
├── _data<br>
│   └── members.yml<br>
│   └── members.csv<br>
├── _drafts<br>
│   ├── begin-with-the-crazy-ideas.md<br>
│   └── on-simplicity-in-technology.md<br>
│   └── hello.md<br>
│   └── world.md<br>
│   └── abcdefg.md<br>
├── _includes<br>
│   ├── footer.html<br>
│   └── header.html<br>
├── _layouts<br>
│   ├── default.html<br>
│   └── post.html<br>
├── _posts<br>
│   ├── 2007-10-29-why-every-programmer-should-play-nethack.md<br>
│   └── 2009-04-26-barcamp-boston-4-roundup.md<br>
│   └── 2020-04-17-hello-world.md<br>
>├── _sass<br>
│   ├── _base.scss<br>
│   └── _layout.scss<br>
├── _site<br>
├── .jekyll-metadata<br>
└── index.html # can also be an 'index.md' with valid front matter

简单归纳表：

|模块|文件夹|内容|作用|备注|
|:-|:--|:-|:-|:-|
|正文|[_posts](https://jekyllrb.com/docs/posts/)|已发布文章.md文件|用于编译生成.html文章|启动时被Jekyll处理生成HTML文件，启动后实时更新内容
|正文|[_drafts](https://jekyllrb.com/docs/posts/#drafts)|未发布文章的.md文件|用于编译生成.html文章|启动时需要加草稿预览参数<br>`--drafts`才会被处理|
|正文|[_data](https://jekyllrb.com/docs/datafiles/)|数据文件| 文章正文可以从这些数据文件里通过变量取值 |支持`.yml`,`.json`,`.csv`和`.tsv`格式，后两者必须包含标题行|
|部署|_site|Jekyll编译生成的静态web资源| 用户直接访问的是这些文件 | 建议.gitignore文件忽略掉它 |
|布局|[_layouts](https://jekyllrb.com/docs/layouts/)|布局.html文件|设计整个静态网站的布局|由主题生成，是主题的组成|
|布局|[_includes](https://jekyllrb.com/docs/includes/)|组件化的局部内容.html文件|用于被其他页面引用|由主题生成，是主题的组成|
|样式|[_sass](https://jekyllrb.com/docs/themes/#understanding-gem-based-themes)|.sass样式文件|编译生成.css|由主题生成，是主题的组成|

除了上面表格里的7大文件夹，还有一个非常重要的知识点 [front matter](https://jekyllrb.com/docs/front-matter/)，它指的是 _post 文章前几行的配置。

今天到此为止，如果使用的时候有疑惑，还是应该再次阅读 [Jekyll官方文档](https://jekyllrb.com/docs/)

----------------2020/04/18----------------

### Jekyll 自定义布局

先去 [Jekyll官方主题网站](http://jekyllthemes.org/) 挑选一个喜欢的主题，下载下来学习 _layouts、_includes、_sass 的写法，我选择了 [Plainwhite](http://jekyllthemes.org/themes/PlainWhite-Jekyll/)：

![Plainwhite主题](https://upload-images.jianshu.io/upload_images/8463645-31272cedfb392805.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

今天只捣鼓了半天，对 _layouts 文件夹的内容有了进一步的了解，收获如下：

|文件|语法|作用域|备注|
|:-|:-|:-|:-|
|default.html|HTML+Liquid|所有页面|含有最上级的<html>标签|
|home.html|HTML+Liquid|首页|使用 html 语法布局，使用 Liquid 语法赋值|
|post.html|HTML+Liquid|所有文章页面|文章必须放到 _posts 或 _drafts 文件夹里|
|page.html|HTML+Liquid|其他非文章页面|例如 about 页|

按照自己的需求改了一下 default.html，网站成了这样，很简洁很喜欢：

![首页](https://upload-images.jianshu.io/upload_images/8463645-62686f28d517c842.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![文章页](https://upload-images.jianshu.io/upload_images/8463645-c3de3cf13728938a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样基本可以投入使用了，但如果仔细看，会发现这个 plainwhite 模板的有些样式似乎还不完善，简洁过度了，我不太喜欢，因此梳理了 TODO List:
* [已解决]表格样式  ——找到<table>样式的位置，进行修改；
* [已解决]引用样式 ——思路同上，对应于<blockquote>标签；
* [已解决]指令样式 ——思路同上，对应于<code>标签；
* [未解决]图片样式（显示图片名） ——思路同上，对应于<img>标签，此步涉及jekyll的编译过程，比较复杂，由于时间成本已超预算，结果导向，先不实现；
* [已解决]大图片CDN化（部署到Github后加载速度慢） ——手动将图片上传至CDN，再引用url，以后如果有闲可以考虑写个markdown图片自动上传并修改小工具；
* [已解决]分类导航 ——这里比较复杂，我暂时解释得不太清楚：[参考资料](https://kylewbanks.com/blog/creating-category-pages-in-jekyll-without-plugins)；



----------------2020/04/20----------------

今日尽力解决了 TODO List，V1.0.0算是完成了，欢迎访问：[https://imzty.github.io/](https://imzty.github.io/)


## 三、我整理的 Jekyll 最佳实践

感谢你坚持看到了这里，下面我会整理出踩过坑的我认为的最佳实践给你：

### 第一步：安装 Jekyll 与环境

1. 安装 Ruby 与 RubyGems，[windows端Ruby官方安装包下载地址](https://rubyinstaller.org/downloads/)；
2. 使用 Ruby 的 gem 指令安装 Jekyll，`gem install jekyll bundler`；
3. 验证安装结果，`jekyll -v`；

### 第二步：去 Jekyll 样式网找一个符合自己口味的样式主题

1. 推荐去 [Jekyll官方样式主题网](http://jekyllthemes.org/) 寻找样式；
2. 下载，解压；
3. 命令行进入解压后的文件夹，运行指令 `bundle exec jekyll serve --trace`；
4. 打开浏览器，访问 [http://localhost:4000](http://localhost:4000/) 查看效果；

### 第三步：对细节进行调整

调整细节，最重要的是要清楚项目各个文件夹的内容有什么用，才能快速找到自己想修改的地方在哪里改才有效：

对于HTML标签的定位：

1. 最上层的页面内容在 _layout 文件夹里的**含有<!DOCTYPE html>标签**的 .html 文件里，一般命名为 default.html；
2. 继承 layout: default 的文件中，主页一般是 home.html，文章详情页一般是 post.html，其他页面一般是 page.html；
3. 如果想根据配置或者文章属性进行取值渲染，可基于 [Liquid](https://shopify.github.io/liquid/basics/introduction/) 语法从 site、page 对象里面取值，可查阅 [Jekyll官方文档之Variables](https://jekyllrb.com/docs/variables/) 获取更多信息；

对于CSS样式的定位：

1. 浏览器访问 [http://localhost:4000](http://localhost:4000/) 后，开启开发者工具寻找某标签样式的出处，再前往该出处文件进行样式修改；

设置分类专用页面，我这里提供一种思路：

1. 在 _layout 文件夹创建你想要的分类布局方式，例如我这里创建为 `sortByCategory.html`，主要关注如何循环取值渲染文章列表；
2. 创建文件夹 `_category`，并在里面创建几个用来存放分类条件的 markdown 文件，每种分类创建一个文件，在这些文件的 front matter 区域写入该文件对应的分类条件，**这里的特异性 front matter 是用来区分不同分类的，将会被** `sortByCategory.html` **从 page 对象获取到，作为条件渲染的条件**，我还建议在这些 markdown 文件里面设置 `permalink` 属性，设置为当前分类页的访问路径；
3. 基于 _config.yml 可以给指定范围的文件设置 front matter 默认值的机制（[官方文档Front Matter Defaults](https://jekyllrb.com/docs/configuration/front-matter-defaults/)），给上一步创建的 markdown 文件设置 layout 默认值，例如我这里设置成 `layout: "sortByCategory"`；
4. 如果 `sortByCategory.html` 的条件渲染逻辑没有异常的话，分类文章列表页面就完成了；

___

#### 结尾

好的，GithubPage + Jekyll 个人博客项目 V1.0.0 到此正式告一段落了，[《项目日记》](/tagSort/project-diary/) 系列是我学习新技术时记录学习过程的文章。此外，由于我一般会在学习新技术的时候，把生活中积累的想法拿出来用新技术实现，所以这个系列还会包含一些有趣想法从构思到实现的过程哦。敬请期待。

![我的微信二维码](https://s1.ax1x.com/2020/05/13/YwZ2X6.jpg)

我是一个自我定位为“喜欢开发有趣工具的Java开发者"，如果对我的文章有任何疑惑或者想交流的地方，欢迎添加我的微信，二维码如上。


