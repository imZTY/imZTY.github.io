---
layout: post
title:  "一篇就够 | 感受PR的基本使用"
date:   2018-08-31 17:01:50 +0800
categories: onePostEnough
permalink: /:categories/:year/:month/:day/:title/
tags: 
- Premiere
- PR入门
- 视频编辑
- 音频编辑
excerpt_separator: <!--more-->
---

本文适用于从未接触过PR的0基础读者，带领读者一起感受PR最基本的使用。
<!--more-->

又是一年新生入学，对于大学城的商家来说又是一波待宰割的小肥羊，而感受过一次新生入学带来的新鲜感的笔者对此不再感到新鲜（或许是看清了一些无聊的规律吧）。然而，即便如此，作为懂一点PR技术的前辈，准备写一篇文章带领新人感受掌握PR技术的必要性，使想要学习这门技术的人们少走一些弯路、节省学习时间。


## 内容预告
前几天刚好做了一个[日语50音图小程序](https://www.jianshu.com/p/ad354d5d3dc1)，其中包含一些音频素材，正好可以用来作为本文的应用场景示例。内容简单，可以跟着一起做。

## 思维导图
![内容纲要](https://upload-images.jianshu.io/upload_images/8463645-1376c6b3490d34d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 一、起步
1. **新建项目**
![新建项目（找个专门的文件夹存放项目，便于统一管理）](https://upload-images.jianshu.io/upload_images/8463645-ffa38475fb5a1e01.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![默认界面各模块的介绍](https://upload-images.jianshu.io/upload_images/8463645-53df44837be335d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. **导入素材**
![右键新建素材箱，并双击打开](https://upload-images.jianshu.io/upload_images/8463645-162b2bb848de8a49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![打开素材箱后右键，选择导入素材（Ctrl+A全选）](https://upload-images.jianshu.io/upload_images/8463645-46520cb2900091b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![导入完成（当然你也可以直接拖拽素材到素材栏的区域里）](https://upload-images.jianshu.io/upload_images/8463645-49ce1909d2802ac4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


3. **建立序列**
![右键新建项目，选择序列](https://upload-images.jianshu.io/upload_images/8463645-e9aadd7c6ae7e059.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

对于新人来说“序列”这个概念可能有点难理解（序列是什么？是个和顺序有关的事物吗？有什么用？），笔者认为“序列”是素材的容器、是交响乐的五线谱，它的作用是制造一个时间轴作为素材摆放的统一标准（例如在那个时间段播放什么素材，又如交响乐里在哪几个小节演奏哪些乐器以及怎样演奏）。

对于交响乐来说，倘若没有统一的节拍（演奏的速度），那么将无法演奏出恢弘壮阔的音乐篇章。而序列就如同一份空白的但是固定了节拍的五线谱、类似一个交响乐的节拍器，而你则是这部交响乐的编辑者。

> [某交响乐专辑](http://music.163.com/album?id=2329697&userid=372473891)

## 二、视频编辑

_大学里时不时会有一些微电影比赛，也时不时会有一些社团活动需要做视频到课室宣传（当然那种视频适合用更专业的特效软件AE来做，这里只是举一些需要编辑视频的场景例子），还有很多想想就知道。可见视频编辑这项技能是经常可以在大学生活里发挥作用的。那么视频编辑包括哪些部分呢？下面就跟着我的演示来感受学习PR的必要性吧。_

* **配音/配乐**
现在，我想做一个卡通动画朗读日语50音的短视频，我想到的方法是：1.从网上找张可爱的卡通图片 2.给这张图片配上一个日语50音的发音音频

  实现过程：
![分别把“小狗图片”和”a.mp3”素材拉到序列的轨道上](https://upload-images.jianshu.io/upload_images/8463645-af445b9077e3c7cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

现在我觉得音轨里的素材太小了，不方便编辑，我想要调整一下音轨可视化的宽度，怎么办？

![按住图中小方格，往左拉（左拉放大，右拉缩小）](https://upload-images.jianshu.io/upload_images/8463645-06aa5543ee5118ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![调整到你想要的程度](https://upload-images.jianshu.io/upload_images/8463645-6bcb894fa01892d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在作品预览栏里点击播放，即可听到小狗发出 あ 的声音，配音环节完成。

![点击播放](https://upload-images.jianshu.io/upload_images/8463645-3aaab5ad2343b545.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


* **裁剪**
配音完成后，我发现音频只有大概 1s，现在我想裁掉那块多出来的“视频”，怎么办？

   方法一（直接编辑一块视频的长度边缘）：
![想裁掉框出的部分](https://upload-images.jianshu.io/upload_images/8463645-acded00ba6f0e440.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![按住视频轨道的边缘，水平向左拖](https://upload-images.jianshu.io/upload_images/8463645-e39ad5fc8716999d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![拖到合适的位置](https://upload-images.jianshu.io/upload_images/8463645-93f4c4fcae799b38.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![方法一裁剪完成（Ctrl+Z 可撤回）](https://upload-images.jianshu.io/upload_images/8463645-fa169e9442f96301.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  方法二（用剃刀工具把视频分成多块，删去多余的块）：

![选择剃刀工具](https://upload-images.jianshu.io/upload_images/8463645-549894ced9965914.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![在合适的位置选择切开](https://upload-images.jianshu.io/upload_images/8463645-3ee5a3c7806002e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![切开后，换回工具箱顶端的选择工具(鼠标)，查看新切得的视频信息](https://upload-images.jianshu.io/upload_images/8463645-8357c372a106856d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![选中要删除的视频，backspace删除，方法二裁剪完成](https://upload-images.jianshu.io/upload_images/8463645-3588c1c4bfca17ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

学会了裁剪，就有能力把一个视频分成多个视频，并再以自己喜欢的顺序任意地重组

* **调速度**
音频中老师念得太快了，我想她念得慢一点，怎么办？

![右键音频/视频，选择"速度/持续时间"](https://upload-images.jianshu.io/upload_images/8463645-b787ef7037864c96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![蓝绿两种方法调速度（保持音频可以避免因速度改变而造成的沉闷音）](https://upload-images.jianshu.io/upload_images/8463645-2329085c352987e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![速度改变后音频/视频的长度会自动调整](https://upload-images.jianshu.io/upload_images/8463645-096a3ac0a1ddc671.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

学会了调速度，就可以抓住视频中的某个细节，进行慢动作播放

* **加字幕**

![在素材栏里右键，选择 新建项目 - 字幕](https://upload-images.jianshu.io/upload_images/8463645-d964bf884ab7c02c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![在默认弹出的字幕编辑窗口里添加字幕文字（这里还有很多需要自行探索的字幕编辑功能）](https://upload-images.jianshu.io/upload_images/8463645-7091e3a23be05a87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![把字幕素材拉到新的视频轨道，并裁剪至合适的长度](https://upload-images.jianshu.io/upload_images/8463645-61ddd86e8dbfbe98.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/8463645-b02210d302300777.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可是现在我发现字幕的位置不太对，怎么办？

![双击字幕素材，使用选择工具，将字幕拖到合适位置](https://upload-images.jianshu.io/upload_images/8463645-eead5a0cc03e4db6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![字幕设置完成](https://upload-images.jianshu.io/upload_images/8463645-196b07d448d23654.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 三、音频编辑
_虽然音频编辑和视频编辑差不多，值得一提的是，音频更适合用素材详情栏进行编辑。_
![双击音频素材即可使音频的详细数据可视化到详细编辑栏里](https://upload-images.jianshu.io/upload_images/8463645-f5211d4803a4a69f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* **裁剪**
同视频

* **调速度**
同视频

* **[录音](http://blog.sina.com.cn/s/blog_486247730102w1fm.html)**
  1.打开音轨混合器
窗口 - 音轨混合器 - 选中当前音轨 - 完成 
![image.png](https://upload-images.jianshu.io/upload_images/8463645-f75dd831cc39b0c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  2.确保音频输入的硬件设置正常（是否已设置麦克风输入）
编辑 - 首选项 - 音频硬件 - ASIO设置 - 勾选输入设备 - 完成
![image.png](https://upload-images.jianshu.io/upload_images/8463645-37980ed8ed4c2671.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/8463645-9195f5f4677f9d9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  3.录制开始
选择一条空白音轨 - 将该音轨设置为录音音轨 - 开启录制模式 - **点击播放按钮**
![image.png](https://upload-images.jianshu.io/upload_images/8463645-a2feaef3d56ca9d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

掌握了视频录音技术，就可以在拍摄微电影的时候对电影进行后期配音了

## 四、总结

整体来说这篇文章挺简单的，虽然笔者并非经常参与视频编辑工作的人，但以上结果功能笔者认为是大学里经常会用到的。


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


