---
layout: post
title:  "一篇就够 | Java校招面试题"
date:   2020-04-22 16:10:31 +0800
categories: onePostEnough
permalink: /:categories/:year/:month/:day/:title/
tags: 
- Java
- 秋招
- 校招
- 面试题
excerpt_separator: <!--more-->
---

这篇文章原本是2019年参加秋招备战时所作，用来积累面试题与答案，后来上岸后去公司实习了，一直到次年4月才最终完成。
<!--more-->

## 前言
*秋招很难顶，9月屡碰壁，笔试拿不到95+%的分数别想面试，面试吃不透本文的题目别想拿offer，抓住国庆假期备战冲一波，以高质量文章造福网友，以写文章的目标与任务鞭策自己。*

*（还有很多题目尚未整理完，后续会继续完善）*



## 内容预告
网友整理的面试问题 + 我自己整理的高质量回答（如果网上能找到质量满意的回答，我愿当复读机，如果没有我会用自己的理解整理出文字来）



## 【一、资料来源】
#### 1.1 问题来源
[Java开发校招面试考点汇总]([https://www.nowcoder.com/discuss/161991](https://www.nowcoder.com/discuss/161991)
)
![上文的整理的考点](https://upload-images.jianshu.io/upload_images/8463645-1b81b4e25f89e258.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 1.2 答案来源
* 大部分答案整理自牛客网同名题目的网友回答；
* 部分答案摘录自极客时间专栏《Java核心技术36讲 - 杨晓峰》；
* 部分答案摘录自慕课网专栏《面试官系统精讲Java源码及大厂真题》；
* 部分答案整理自各博客平台的公开文章；

___


## 【二、我的答案】

### 一、JavaSE部分

#### **❤1、Java基础**

1、为什么重写equals还要重写hashcode
>1. 首先从业务场景出发，当需要重写 equals() 时，说明判断对象是否相等的标准从“判断内存地址是否相等”转为了“判断值内容是否相等”；
>2. 此时，如果只是重写了 equals() 方法，hashCode() 仍是以“内存地址”来作为生成返回值的标准，如果不改变的话，将会那些使用了 Hash 机制进行效率优化的集合类（HashSet、HashMap等）出现与业务需求不一致的现象 —— 因为例如在判断 key 是否相等或是否已存在时，旧的判断指标是“内存是否相等”（默认如此），而新的需求是要按“内容相等”作为指标；
>3. 所以，为了确保相同的 key 在 hash集合中的映射具有唯一性，为了使那些 Hash 集合类能够按照新的需求发挥作用，重写 equals() 后还需要重写 hashCode()；
[参考文章](https://www.oschina.net/question/82993_75533)

2、说一下常见的Map和List
>![我整理的](https://upload-images.jianshu.io/upload_images/8463645-9c283d5d25b7ee88.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


3、Object若不重写hashCode()的话，hashCode()如何计算出来的？
>Object 的 hashcode 方法是本地方法，也就是用 c 语言或 c++ 实现的，该方法直接返回对象的 内存地址

4、==比较的是什么？
>若是基本类型或基本类型的包装类，则比较值内容；
若是引用类型(如对象)，则比较内存地址；

5、若对一个类不重写，它的equals()方法是如何比较的？
> return (this == obj);   //Object类默认比较内存地址

6、java8新特性
>（新特性有很多，每一个新特性都有很多内容，我这里不细说， [参考文章](https://www.cnblogs.com/onetwo/p/8526374.html)）
>* default 关键字使接口类也可以包含方法的默认实现；
>* Lambda 表达式
>* 函数式接口
>* 函数的引用（方法与构造函数的引用）
>* 支持运行JavaScript（Nashorn引擎）
>* Date/Time API（Clock、LocalTime）
>* Stream
>* 官方库已新增支持Base64编码

7、说说Lamda表达式的优缺点。

> ###### 优点：
>* 代码简洁，开发迅速
>* 方便函数式编程
>* 容易进行并行计算
>* java引入lambda，改善了集合操作（引入Stream API）
>###### 缺点：
>* 影响代码可读性，要求读者也懂Lambda
>* 性能方面，在非并行计算中，很多计算未必有传统的for性能要高
>* 不容易进行调试


8、一个十进制的数在内存中是怎么存的？
>二进制补码

9、为啥有时会出现4.0-3.6=0.40000001这种现象？
>因使用二进制表示小数所造成的误差

10、Java支持的数据类型有哪些？什么是自动拆装箱？
>![基本数据类型](https://upload-images.jianshu.io/upload_images/8463645-d74179536a595374.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
自动拆装箱：基本数据类型与其包装类之间的自动转换，在编译过程实现；[参考文章](https://www.cnblogs.com/dolphin0520/p/3780005.html)



11、什么是值传递和引用传递？
>* 传递指将实际内容传递给函数定义时声明的形式参数处；
>* 若是数值类型则使用值传递（基本数据类型），若是引用类型则使用引用传递（对象类型）；
>* 基本数据类型存储于栈帧中，传递时传递其值的复制，不影响上一层的内容；
>* 所有对象的实际内容都存放在堆里，而引用类型在栈帧中存储的是指向对象堆中的地址，所以传递时将地址传过去后所引发的修改会直接改变堆中对象的内容，会影响上一层的内容；

12、数组(Array)和列表(ArrayList)有什么区别？什么时候应该使用Array而不是ArrayList？
>|区别 | Array | ArrayList |
>|:-|:--|:--|
>| 内容 | 支持基本类型和对象 | 只能是对象类型 |
>| 容量 | 定长，需要提前声明 | 动态调整，溢出时默认增加50%长度 |
>| 方法 | 无内置方法 | 有内置方法，如addAll()，iterator() |

13、你了解大O符号(big-O notation)么？你能给出不同数据结构的例子么？
>大O符号表示一个程序运行时所需要的渐进时间复杂度上界（即最小的最坏情况），可以用来描述算法运算量的情况

14、String是最基本的数据类型吗?
>不，它是引用数据类型；

15、int 和 Integer 有什么区别
>int是基本数据类型， Integer是包装类 ；
int的速度快，Integer的速度慢；
int放在栈中，Integer放在堆中；
int初始值为0，Integer初始值为null；

16、String 和StringBuffer的区别
>String是final类，一旦赋值无法改变；
StringBuffer是线程安全的字符串拼接缓冲类，有同步锁，性能较慢；
StringBuild是非线程安全的字符串拼接缓冲类，没有同步锁，性能快；

17、我们在web应用开发过程中经常遇到输出某种编码的字符，如iso8859-1等，如何输出一个某种编码的字符串？
>new String(str.getBytes("ISO-8859-1"), "GBK");   //编码格式1 编码格式2

18、int和Integer有什么区别？
>int 是基本数据类型，数据存放在栈帧，没有封装方法；
Integer 是 int 的包装类，数据放在对象堆，有内部方法，他们之间的转换有自动拆装箱机制；

19、&和&&的区别？
>&可以逻辑运算且，还可以位运算求与，不可短路判断逻辑，必须计算完两边的逻辑；
>&&只能逻辑运算，可以短路判断逻辑，若前者逻辑可以得知结果，则不再计算后者；

20、在Java中，如何跳出当前的多重嵌套循环？
>在嵌套开始时，用 [标号]+[英文冒号] 的语法创建标号，需要退出时，使用 break [标号];

21、你能比较一下Java和JavaSciprt吗？
>java:面向对象;需要编译，再进行运行;强类型.
javascript:基于对象和事件驱动;解释型语言;弱类型

22、简述正则表达式及其用途。
>一套字符串匹配规则的规范，用于字符串匹配，如同润滑油一般顺滑

23、Java中是如何支持正则表达式操作的？
>相关方法：matches()、replaceAll()、replaceFirst()、split()
相关类：Pattern、Matcher

24、请你说说Java和PHP的区别？
>从应用的角度来看：PHP适合于快速开发，适用于中小型应用系统，开发成本低，能够对变动的需求作出快速的反应。而Java的可拓展性更强，既适用于小型项目，也支持中型/大型的应用开发，适合于开发大型的应用系统，应用的前景比较广阔，系统易维护、可复用性较好

#### **❤2、关键字**

1、介绍一下Syncronized锁，如果用这个关键字修饰一个静态方法，锁住了什么？如果修饰成员方法，锁住了什么？
>对于普通的同步方法： 锁是当前的对象（创建的实例）
对于静态函数的同步方法： 锁是指引用当前类的class对象
对于同步方法块的内容： 锁是指Synchonized括号里配置的对象

2、介绍一下volatile？
>广播通知各线程，更新CPU缓存，重新从内存中读取修改后的volatile变量；
即使加了volatile，修改操作仍具有线程不安全性

3、锁有了解嘛，说一下Synchronized和lock
>synchronized是隐式锁，Lock是锁的接口类是显式锁，需要自己实现加锁与解锁的逻辑；
当线程数量增多时，隐私锁的性能将大幅度下降，显式锁影响不大，显式锁性能更稳定；

4、讲一讲Java里面的final关键字怎么用的？
>用在类上，该类无法被继承；
用在方法上，该方法无法被重写；
用在变量上，变量必须初始化且后续无法改变其内容；

 #### **❤3、面向对象**

1、wait方法底层原理
>由ObjectMonitor 添加到 _WaitSet，释放所有锁，等待被唤醒

2、Java有哪些特性，举个多态的例子。
>封装，继承，多态
其中方法的重写、重载、向上转型都与多态有关
>___
>封装：隐藏事务内部的实现细节，以便提高安全性和简化编程。
继承：是代码复用的基础机制，类似于我们对马、白马、黑马的总结。
多态：重写=父子类中同名同参方法的不同实现，重载=同名不同参的方法。

3、String为啥不可变？
>因为它是个final类，无法被继承，且实例一旦完成初始化，将无法修改值的内容

4、类和对象的区别
>类是对象的抽象，对象时类的实例

5、请列举你所知道的Object类的方法。
>clone() 创建并返回此对象的一个副本。
equals(Object obj) 指示其他某个对象是否与此对象“相等”。
getClass() 返回此 Object 的运行时类。
hashCode()返回该对象的哈希码值。
notify() 唤醒在此对象监视器上等待的单个线程
notifyAll() 唤醒在此对象监视器上等待的所有线程。
toString() 返回该对象的字符串表示。
wait() 在其他线程调用此对象的 notify() 方法或 notifyAll() 方法前，导致当前线程等待。
finalize() 用于释放资源，可以覆盖此方法实现资源清理工作。GC在回收对象之前调用


6、重载和重写的区别？相同参数不同返回值能重载吗？
>重写:子类重写父类的方法，重载:同名不同参；不可以

7、”static”关键字是什么意思？Java中是否可以覆盖(override)一个private或者是static的方法？
>“static”关键字表明一个成员变量或者是成员方法可以在没有所属的类的实例变量的情况下被访问。  Java中static方法不能被覆盖，因为方法覆盖是基于运行时动态绑定的，而static方法是编译时静态绑定的。private权限私有无法被其他类访问。


8、String能继承吗？
>不能，因为被final修饰的类无法被继承，且实例一旦完成初始化，值的内容也无法被修改

9、StringBuffer和StringBuilder有什么区别，底层实现上呢？
>String是final类，一旦赋值无法改变；
StringBuffer是线程安全的字符串拼接缓冲类，有同步锁，性能较慢；
StringBuild是非线程安全的字符串拼接缓冲类，没有同步锁，性能快；

10、类加载机制，双亲委派模型，好处是什么？
>“双亲委派模式”我觉得翻译得不好，更应翻译为父类委派模型
>
>JVM类加载器从上到下一共分为三类 
1\.启动类加载器(Bootstrap ClassLoader)：负责加载 JAVA_HOME\lib 目录中的，或通过-Xbootclasspath参数指定路径中的，且被虚拟机认可（按文件名识别，如rt.jar）的类。 
2\. 扩展类加载器(Extension ClassLoader)：负责加载 JAVA_HOME\lib\ext 目录中的，或通过java.ext.dirs系统变量指定路径中的类库。 
3\. 应用程序类加载器(Application ClassLoader)：负责加载用户路径（classpath）上的类库。
>
>双亲委派模型是每次收到类加载请求时，先将请求委派给父类加载器完成，如果父类加载器无法完成加载，那么子类尝试自己加载。好处是：不管哪个加载器加载这个类，最终都是委托给顶层的启动加载器加载这个类，这样就保证了使用不用的类加载器最终得到的都是同样的Object对象
>___
>* 类加载机制：虚拟机把描述类的数据从class文件加载到内存，并对数据进行校验、转换解析和初始化，最终形成可以被虚拟机直接使用的Java类型。
>
>* 类加载时机：类的生命周期是从类被加载到虚拟机内存中，到卸载内存为止。
>
> * 类的生命周期：加载 loading ---> 连接(验证 verification 准备 preparation 解析 resolution) ---> 初始化 initialization ---> 使用 using --- > 卸载 unloading
>
>* 类加载过程
      [加载]
          1.从Class文件获取二进制字节流
          2.将字节流中的静态结构转化为方法区的运行时的动态结构
          3.在内存中生成代表该Class的java.lang.Class对象，作为方法区该类的访问入口。
      [连接]
          1.验证：验证Class文件的字节流中包含的信息是否符合JVM的要求，并确保不会危害JVM自身的安全。
          2.准备：为静态变量分配内存并赋初始值
          3.解析：将常量池内的符号引用转换为直接引用
      [初始化]
>    调用类的clinit()方法，为静态变量赋予实际的值，执行静态代码块




11、静态变量存在哪?
>以前存放在方法区(也有称全局区)，但JDK8之后就取消了“永久代”，取而代之的是“元空间”，永久代中的数据也进行了迁移，**静态成员变量迁移到了堆中**（方法区是JVM的规范，永久代是方法区的具体实现）。

12、讲讲什么是泛型？
>简单概括是一种约定。泛型多用于容器中，往容器中方数据，事先约定什么类型数据，放的时候会检查，不是正确的类型放入时会报错，这样可以建立安全的数据，也避免了强制类型转换

13、解释extends 和super 泛型限定符-上界不存下界不取
>extends上限通配符，用来限制类型的上限，必须是该类的子类；
super下限通配符，用来限制类型的下限，必须是该类的父类；

14、是否可以在static环境中访问非static变量？
>不可以，这是静态内容与类加载的问题，因为static的内容不需要创建实例，它会随着其所在类被加载到堆区，非static的内容必须创建其所在类的实例才能被访问。当类加载时，此时不一定有实例创建，没有实例，就不可以访问非静态的成员。

15、谈谈如何通过反射创建对象？
>Object obj = Class.forName(className).newInstance();

16、Java支持多继承么？
>不支持，子类只能有一个父类，但可以实现多个接口类；

17、接口和抽象类的区别是什么？
>接口类主要用于：将API定义与API实现进行分离；
抽象类主要用于：代码重用；

18、Comparable和Comparator接口是干什么的？列出它们的区别。
>是用于对数据集合进行比较或排序的

19、面向对象的特征有哪些方面
>封装：隐藏事务内部的实现细节，以便提高安全性和简化编程。
继承：是代码复用的基础机制，类似于我们对马、白马、黑马的总结。
多态：重写=父子类中同名同参方法的不同实现，重载=同名不同参的方法。

20、final, finally, finalize的区别。
>final：给被修饰的事物赋予不可改变性
>finally：用于 try-catch 结束后的收尾工作
>finalize：与GC内存回收相关

21、Overload和Override的区别。Overloaded的方法是否可以改变返回值的类型?
>Override:子类重写父类的方法，Overload:同名不同参；不可以

22、abstract class和interface有什么区别?
>接口类主要用于：将API定义与API实现进行分离；
抽象类主要用于：代码重用；

23、Static Nested Class 和 Inner Class的不同
>静态嵌套类可以通过 [所属类名]+[嵌套类名] 被具有权限的外部获取，如 new OutClass.NestedClass()；
内部类必须在所属类创建的对象的基础上，通过 [对象名]+ . +[内部类名] 来生成，如 outObject.new Inner();

24、当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递?
>我认为这是一种“以值传递的形式实现的引用传递”。之所以说是值传递，是因为传入参数并没有改变，传输的只是其值的复制，传入参数存放的是对象数据在堆内的地址；之所以又说是引用传递，是因为虽然参数的具体内容没有受到影响，但是它表示的对象的数据内容是改变了的，我认为抽象地看属于引用传递；
>___
>这里我觉得站在不同的角度有不同的答案。我一开始认为是引用传递，因为对象传递进去后方法修改其内容，存储在堆里的内容数据被改变了，会对原来调用该方法那个栈帧里的原对象造成内容改变，所以是引用传递。但是网上的回答，都是说值传递，传递的值的对象数据所在内存的地址的复制，方法会改变对象数据的内容，但原对象的地址没有改变。争议点在于"值传递"是狭义地认为传入参数有没有受到影响，还是应该判断传入参数的抽象内容有没有受到影响。最后我觉得用“以值传递的形式实现的引用传递”来描述比较符合我自己的理解。

25、Java的接口和C++的虚类的相同和不同处。
>c++的虚类相当于java中的抽象类：
相同点：都不能实例化；
不同点：（1）抽象类可以有构造方法，接口没有构造方法；
（2）抽象类可以用private，protected，public，default修饰，接口只能用public来修饰；
（3）抽象类有抽象方法和非抽象方法，而接口只有抽象方法，接口是一种更特殊的抽象类；
（4）子类只能继承一个抽象类，但可以实现多个接口；

26、JAVA语言如何进行异常处理，关键字：throws,throw,try,catch,finally分别代表什么意义？在try块中可以抛出异常吗？
>throws：是说明可能会出现哪些异常的指令，在定义方法时声明
throw：是主动抛出异常的指令
try：常常以 try-catch-finally 的形式出现，try负责声明哪些语句可能会出现异常且需要监听，用大括号将它们框起来
catch：常常以 try-catch-finally 的形式出现，catch负责声明并截获try模块中出现的指定异常，并用大括号将该异常的处理语句框起来
finally：常常以 try-catch-finally 的形式出现，finally负责声明不论是否有异常都会执行的语句，常常用于释放资源等收尾善后工作
>
>不可以

27、内部类可以引用他包含类的成员吗？有没有什么限制？
>如果不是静态内部类，完全可以。那没有什么限制！ 
在静态内部类下，不可以访问外部类的普通成员变量，而只能访问外部类中的静态成员

28、两个对象值相同(x.equals(y) == true)，但却可有不同的hash code说法是否正确？
>在默认情况下是错误的。但如果这个人重写了equals()没有重写hashCode()的话，会出现上述情况，这个说法也可以是正确的。

29、重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？
>Override:子类重写父类的方法，Overload:同名不同参；不可以

30、如何通过反射获取和设置对象私有字段的值？
>Class.getDeclaredFields()

31、谈一下面向对象的"六原则一法则"。
>S.O.L.I.D.  C.
迪米特法则
>___
>[参考文章](https://www.cnblogs.com/shanyou/archive/2009/09/21/1570716.html)
>1. 单一职责原则（Single Responsibility Principle ）：一个类只做它该做的事情。（单一职责原则想表达的就是"高内聚"，写代码最终极的原则只有六个字"高内聚、低耦合"，所谓的高内聚就是一个代码模块只完成一项功能，在面向对象中，如果只让一个类完成它该做的事，而不涉及与它无关的领域就是践行了高内聚的原则，这个类就只有单一职责。
>2. 开闭原则（Open Closed Principle ）：软件实体应当对扩展开放，对修改关闭。（在理想的状态下，当我们需要为一个软件系统增加新功能时，只需要从原来的系统派生出一些新类就可以，不需要修改原来的任何一行代码。要做到开闭有两个要点：①抽象是关键，一个系统中如果没有抽象类或接口系统就没有扩展点；②封装可变性，将系统中的各种可变因素封装到一个继承结构中，如果多个可变因素混杂在一起，系统将变得复杂而混乱。
>3. 里氏替换原则（Liskov Substitution Principle）：任何时候都可以用子类型替换掉父类型。但简单的说就是能用父类型的地方就一定能使用子类型。里氏替换原则可以检查继承关系是否合理，如果一个继承关系违背了里氏替换原则，那么这个继承关系一定是错误的，需要对代码进行重构。
>4. 接口隔离原则（Interface Segregation Principle）：接口要小而专，避免大而全。
>5. 依赖倒转原则（Dependency Inversion Principle）：面向接口编程。（该原则说得直白和具体一些就是声明方法的参数类型、方法的返回类型、变量的引用类型时，尽可能使用抽象类型而不用具体类型，因为抽象类型可以被它的任何一个子类型所替代。
>6. 复合聚合复用原则（Composite/Aggregate Reuse Principle）：优先使用聚合或合成关系复用代码。要说明的是，即使在Java的API中也有不少滥用继承的例子，例如Properties类继承了Hashtable类，Stack类继承了Vector类，这些继承明显就是错误的，更好的做法是在Properties类中放置一个Hashtable类型的成员并且将其键和值都设置为字符串来存储数据，而Stack类的设计也应该是在Stack类中放一个Vector对象来存储数据。记住：任何时候都不要继承工具类，工具是可以拥有并可以使用的，而不是拿来继承的。） 
> * [迪米特法则]([https://www.jianshu.com/p/081403a945dd](https://www.jianshu.com/p/081403a945dd)
)（Law of Demeter）：迪米特法则又叫最少知识原则，一个对象应当对其他对象有尽可能少的了解。



32、请问Query接口的list方法和iterate方法有什么区别？
>1.返回的类型不一样，list返回List，iterate返回iterator 
2.查询策略不同。获取数据的方式不一样，list会直接查询数据库，iterate会先到数据库中把id取出来，然后真正要遍历某个对象的时候先到缓存中找，如果找不到，以id为条件再发一条sql到数据库，这样如果缓存中没有数据，则查询数据库的次数为n+1
3.iterate会查询2级缓存，list只会缓存，但不会使用缓存（除非结合查询缓存）。
4.list中返回的list中每个对象都是原本的对象，iterate中返回的对象是代理对象

33、Java中的方法覆盖(Overriding)和方法重载(Overloading)是什么意思？
>Override:子类重写父类的方法，Overload:同名不同参；

34、Java中，什么是构造函数？什么是构造函数重载？什么是复制构造函数？
>* Java中的构造函数是为了初始化对象的，构造函数的函数名和类名一致，没有返回值；默认的构造函数没有参数、函数体也没有内容。
>* 构造函数的重载是函数名与类名相同，参数类型不同，参数不同。同样的作用也是为了初始化对象的。
>* 与C++不同，由于Java所有对象的值都是对象数据的存放地址，Java中没有拷贝构造函数的概念，Java不需要考虑需要使用复制构造函数这种问题，有其他复制方案。

35、hashCode()和equals()方法有什么联系？
>重写equals()后，最好也要重写hashCode()
>___
>如果 x.equals(y) 返回 “true”，那么 x 和 y 的 hashCode() 必须相等 ；
 如果 x.equals(y) 返回 “false”，那么 x 和 y 的 hashCode() 有可能相等，也有可能不等 ；
 如果 x 和 y 的 hashCode() 不相等，那么 x.equals(y) 一定返回 “false” ；


#### **❤4、集合**

1、Map和ConcurrentHashMap的区别？
>Map：一种键值对集合接口类
ConcurrentHashMap：分段上锁的线程安全Map集合实现类。可以理解为类似16个线程安全的hashtable组合成了一个concurrenthashmap，不同分段操作不需要上锁，同一个分段才需要上锁，读不上锁，写上锁。锁的粒度更加精细。而1.8采取的AQS和CAS来实现【用了不少volatile】

2、hashMap内部具体如何实现的？
>* 首先，HashMap有一个定长的结点数组，利用Hash映射，计算key的hash码，并根据hash码决定key结点在数组中的的存放位置，这样做的好处是可以实现降维的效果；
>* 由于Hash映射是多对一的关系，不同的数据可能得到相同的hash码，对于这种情况，HashMap会改变数组结点的数据结构来存放那些相同hash码但内容不同的数据；当相同hash的结点数量少于6时，HashMap默认使用链表来存放这些结点，数组里的结点是链表头；当相同hash的结点数量大于8时，原来的链表会转换成红黑树进行存储，数组里的结点是树根；
>___
>###### 红黑树新增结点的过程：
>1. 首先判断新增的节点在红黑树上是不是已经存在,判断手段有如下两种: 
>1.1. 如果节点没有实现 Comparable 接口,使用 equals 进行判断;
>1.2. 如果节点自己实现了 Comparable 接口,使用 compareTo 进行判断;
>2. 新增的节点如果已经在红黑树上，直接返回；不在的话，判断新增节点是在当前节点的左边还是右边，左边值小，右边值大；
>3. 自旋递归 1 和 2 步，直到当前节点的左边或者右边的节点为空时，停止自旋，当前节点即为我们新增节点的父节点；
>4. 把新增节点放到当前节点的左边或右边为空的地方，并于当前节点建立父子节点关系；
>5. 进行着色和旋转，结束。
>
>###### 红黑树的5个原则：
>* 节点是红色或黑色
>* 根是黑色
>* 所有叶子都是黑色
>* 从任一节点到其每个叶子的所有简单路径都包含相同数目的黑色节点
>* 从每个叶子到根的所有路径上不能有两个连续的红色节点

3、如果hashMap的key是一个自定义的类，怎么办？
>如果需要重写该类的equals()方法，则必须同时修改hashCode()方法

4、ArrayList和LinkedList的区别，如果一直在list的尾部添加元素，用哪个效率高？
>ArrayList：动态数组。扩容时，每次延长50%，即1.5倍。![ArrayList数据结构](https://upload-images.jianshu.io/upload_images/8463645-77d0cd6022bdc985.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
LinkedList：双向链表。每次新增结点时，new 一个Node。![LinkedList数据结构](https://upload-images.jianshu.io/upload_images/8463645-04ed4680c3b6278c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>插入的效率并不是LinkedList恒优于ArrayList，当new对象的效率比ArrayList数组扩容的单位平均效率慢时，ArrayList比LinkedList快；反之则慢；网上的说法是，数据量上到千万级时会出现这样的情况，我认为是JVM堆内存不足所造成的，业务场景似乎不太现实，如果开发设计得合理的话，很难想象生活中哪里会有这样的场景

5、HashMap底层，负载因子，为啥是2^n？
>这里的2^n负载因子，其实是指容量。原因是因为公式：K%N == K&(N-1)……当N=2^n时成立；这样的好处是可以更快地进行求模运算。

6、ConcurrentHashMap锁加在了哪些地方？
>1.7在代码段，1.8再hash数组的头结点处；1.8的锁粒度比1.7小得多；

7、TreeMap底层，红黑树原理？
>TreeMap 利用了红黑树左节点小，右节点大的性质，根据 key 进行排序，使每个元素能够插入到红黑树大小适当的位置，维护了 key 的大小关系，适用于 key 需要排序的场景。
因为底层使用的是平衡红黑树的结构，所以 containsKey、get、put、remove 等方法的时间复杂度都是 log(n)。
红黑树原理：平衡二叉树
>___
>###### [几种二叉树的定义](https://stackoverflow.com/questions/12359660/difference-between-complete-binary-tree-strict-binary-tree-full-binary-tre)：
>* 完美二叉树：所有非叶子结点，都有两个子节点；且每一层都被填满了；
>* (完)满二叉树：所有非叶子结点，都有两个子节点；
>* 完全二叉树：除了最后一层外的每一层必须被填满；且最后一层严格左对齐；
>* 平衡二叉树：左右子树深度绝对值相差小于2；

8、concurrenthashmap有啥优势，1.7，1.8区别？
>concurrenthashmap是hashmap的多线程版本
>
>jdk1.7中采用Segment + HashEntry的方式进行实现
>
>1.8中放弃了Segment臃肿的设计，取而代之的是采用Node + CAS + Synchronized来保证并发安全进行实现


9、ArrayList是否会越界？
>可能会越界，因为它不是线程安全的。在多线程操作同一个ArrayList的时候，两个线程同时执行Add在线程1已经将size++而线程二在读取的时候导致越界 线程在被挂起的时候，执行的位置不一样 Size是个共有变量 自增是个非原子操作


10、什么是TreeMap?
>TreeMap继承AbstractMap，实现NavigableMap、Cloneable、Serializable三个接口，支持顺序遍历和逆序遍历；数据结构采用红黑树

11、ConcurrentHashMap的原理是什么？
>concurrenthashmap是hashmap的多线程版本
>
>jdk1.7中采用Segment + HashEntry的方式进行实现
>
>1.8中放弃了Segment臃肿的设计，取而代之的是采用Node + CAS + Synchronized来保证并发安全进行实现

12、Java集合类框架的基本接口有哪些？
>Collection
>Collection.List
>Collection.Set
>Map

13、为什么集合类没有实现Cloneable和Serializable接口？
>这个问题说的不清楚，集合类框架中的接口没有实现Cloneable和Serializable接口，但是具体的实现类是实现了这些接口的，比如Arraylist

14、什么是迭代器？
>是一种用于遍历数据集合的设计模式

15、Iterator和ListIterator的区别是什么？
>1. Iterator和ListIterator的区别是：  Iterator可用来遍历Set和List集合，但是ListIterator只能用来遍历List
>2. Iterator对集合只能是前向遍历，ListIterator既可以前向也可以后向

16、快速失败(fail-fast)和安全失败(fail-safe)的区别是什么？
>快速失败：当你在迭代一个集合的时候，如果有另一个线程正在修改你正在访问的那个集合时，就会抛出一个ConcurrentModification异常。（同时修改异常）
>
>    在java.util包下的都是快速失败。
>
>（原理：迭代器在遍历时直接访问集合中的内容，并且在遍历过程中使用一个 modCount 变量。集合在被遍历期间如果内容发生变化，就会改变modCount的值。每当迭代器使用hashNext()/next()遍历下一个元素之前，都会检测modCount变量是否为expectedmodCount值，是的话就返回遍历；否则抛出异常，终止遍历）
>___
>安全失败：在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历，所以你在修改上层集合的时候是不会受影响的，不会抛出ConcurrentModification异常。
>
>    在java.util.concurrent包下的全是安全失败的。


17、HashMap和Hashtable有什么区别？
>|区别 | HashMap | Hashtable |
>|:-|:--|:--|
>| 线程安全性 | 非线程安全 | 线程安全 |
>| 是否支持键null | 支持 | 不支持 |
>| 性能效率 | 快 | 慢（同步有开销） |
>| 适用场景 | 单线程 | 多线程 |
> （其实多线程也轮不到Hashtable，多线程用ConcurrentHashMap更好）

18、ArrayList和LinkedList有什么区别？
>|区别 | ArrayList | LinkedList |
>|:-|:--|:--|
>| 线程安全性 | 非线程安全 | 非线程安全 |
>| 擅长 | 查询（有索引） | 增删（无索引） |
>| 数据结构 | 动态数组 | 双向链表 |
>
>（插入的效率并不是LinkedList恒优于ArrayList，当new对象的效率比ArrayList数组扩容的单位平均效率慢时，ArrayList比LinkedList快；反之则慢；网上的说法是，数据量上到千万级时会出现这样的情况，我认为是JVM堆内存不足所造成的，业务场景似乎不太现实，如果开发设计得合理的话，很难想象生活中哪里会有这样的场景）

19、ArrayList,Vector,LinkedList的存储性能和特性是什么？
>插入性能：Vector < ArrayList < LinkedList
>查询性能：Vector < LinkedList < ArrayList
>
>特性：Vector具有线程安全性，LinkedList 和 ArrayList 都不具有线程安全性

20、Collection 和 Collections的区别。
>Collection是java.util下的接口，它是各种集合结构的父接口，继承于它的接口的主要有set和List，提供关于集合的一些操作，比如插入、删除、判断一个元素是否是其成员，遍历等。
>
>Collections是java.utis下的类，是针对集合类的一个工具类，提供一系列静态方法，实现对集合的查找、排序、替换、线程安全(将非同步的集合转换成同步的)等操作。


21、你所知道的集合类都有哪些？主要方法？
>![我整理的](https://upload-images.jianshu.io/upload_images/8463645-9c283d5d25b7ee88.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>主要方法：.iterator()、.size()、.add()、.get()、.remove()、.addAll()、.isEmpty()、keySet()

22、List、Set、Map是否继承自Collection接口？
>Map不是

23、阐述ArrayList、Vector、LinkedList的存储性能和特性
>插入性能：Vector < ArrayList < LinkedList
>查询性能：Vector < LinkedList < ArrayList
>
>特性：Vector具有线程安全性，LinkedList 和 ArrayList 都不具有线程安全性

24、List、Map、Set三个接口存取元素时，各有什么特点？
>List集合有序可重复
>Set集合无序不重复
>Map集合是键值对映射，值可以重复，但键不可以重复；Map可以获取keySet

#### **❤5、线程**

1、多线程中的i++线程安全吗？为什么？
>不安全，因为它并不具备原子性，它的过程分为：从CPU缓存或内存读取 i 的值、和 将修改后的值 i = i + 1 写入内存

2、如何线程安全的实现一个计数器？
>有三种方案，分别是：
>方案1：使用基本数据类型的原子类存放计数量；![底层原理是CAS](https://upload-images.jianshu.io/upload_images/8463645-44a485fa7364b62b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>
>方案2：使用同步关键字 synchronized 取消计数逻辑的异步不安全性；
>方案3：使用 Lock 的具体实现类自主管理资源锁，这样做的性能会比 synchronized 方案要高，因为节省了一些隐式的开销；
>___
>顺便提一下 [volatile](https://mp.weixin.qq.com/s?__biz=MzIxMjE5MTE1Nw==&mid=2653192450&idx=2&sn=ad95717051c0c4af83923b736a5bc637&chksm=8c99f3d8bbee7aceb123e4f6aa9a220630b5aa17743ba812d82308bfb6a8ed8303bdd181f144&mpshare=1&scene=1&srcid=1008I6TLQnTyffD6XVSpvSTU&sharer_sharetime=1570533699629&sharer_shareid=7b8597c48826f06dfb6dffb1448a4422&key=abef5ca5ef94578d3c6b80d8f92f1970a33f3db3c2d4563b643592774d9edf5a702e4f83575e40b92187858ecf79c31a6a40d35280444d53a82b2408f6dd787ef28fdce9a8cd7b8252ae66be8edc9330&ascene=1&uin=MTU1MTAxNTkxMg%3D%3D&devicetype=Windows+7&version=62070141&lang=zh_CN&pass_ticket=9zkPgtqmJic%2Bg%2BfGpkfiR3fYe94Oofzzu4qTN4CVrN2VDWC%2BLv8dpm%2F9xV%2BFpr6t) 关键字，它可以确保CPU缓存里的数据是主存里最新的（可见性），还引入内存屏障实现了阻止指令重排。但它不能确保线程安全性。

3、多线程同步的方法
>原子类(CAS)、synchronized、Lock

4、介绍一下生产者消费者模式？
>设置任务信息量，并分别设置创建任务信息的逻辑模块、处理任务信息的逻辑模块。
>这样一来，任务信息的创建与处理可以实现解耦，同时还可以异步同时进行。

5、线程，进程，然后线程创建有很大开销，怎么优化？
>使用线程池管理线程资源，重复利用已创建的线程，避免了销毁线程时的开销，减少了创建新线程的次数与创建时的开销，而且这样一来相应的速度也将变得更快；此外还可以提高线程的可管理性；

6、线程池运行流程，参数，策略
>###### 流程
>![牛客网上的一个回答](https://upload-images.jianshu.io/upload_images/8463645-b44ec1eb65fcb65b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>###### 参数
>* corePoolSize，所谓的核心线程数，可以大致理解为长期驻留的线程数目（除非设置了 allowCoreThreadTimeOut）。对于不同的线程池，这个值可能会有很大区别，比如 newFixedThreadPool 会将其设置为 nThreads，而对于 newCachedThreadPool 则是为 0。
>* maximumPoolSize，顾名思义，就是线程不够时能够创建的最大线程数。同样进行对比，对于 newFixedThreadPool，当然就是 nThreads，因为其要求是固定大小，而 newCachedThreadPool 则是 Integer.MAX_VALUE。
>* keepAliveTime 和 TimeUnit，这两个参数指定了额外的线程能够闲置多久，显然有些线程池不需要它。
>* workQueue，工作队列，必须是 BlockingQueue。
>###### 策略
>* 大小的选择策略：（1）对于计算密集型的业务，建议将线程池的最大容量设置为 N 或 N+1，N 是CPU的核数；（2）对于需要较多等待的 I/O 密集型的业务，可以参考 Brain Goetz 推荐的计算方法：
>``` 
>线程数 = CPU核数 × 目标CPU利用率 ×（1 + 平均等待时间 / 平均工作时间）
> ```
>* 如果任务量远远大于线程池的线程容量，可能会导致任务队列发送OOM，开发时要考虑实际业务可能发送的极端情况；

7、讲一下AQS吧。
>[AQS](https://docs.oracle.com/javase/9/docs/api/java/util/concurrent/locks/AbstractQueuedSynchronizer.html)（Class AbstractQueuedSynchronizer），是java并发包中的核心类，诸如ReentrantLock，CountDownLatch等工具内部都使用了AQS去维护锁的获取与释放：

8、创建线程的方法，哪个更好，为什么？
>1、继承Thread类，重载run()方法；
>2、实现Runnable接口，实现run()方法，实现Runnalbe接口更好，使用实现Runnable接口的方式创建的线程可以处理同一资源，从而实现资源的共享（为什么？）

9、Java中有几种方式启动一个线程？
>1、继承Thread类  2、实现Runnable 接口 3、实现callable接口  4、线程池的方式开启线程

10、Java中有几种线程池？
>* newCachedThreadPool()：创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程
>* newFixedThreadPool(int nThreads)：创建一个指定工作线程数量的线程池。每当提交一个任务就创建一个工作线程，如果工作线程数量达到线程池初始的最大数，则将提交的任务存入到池队列中。
>* newSingleThreadExecutor()：创建一个单线程化的Executor，即只创建唯一的工作者线程来执行任务，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。如果这个线程异常结束，会有另一个取代它，保证顺序执行。
>* newScheduleThreadPool()：创建一个定长的线程池，而且支持定时的以及周期性的任务执行，支持定时及周期性任务执行。
>* newWorkStealingPool(int parallelism)，这是一个经常被人忽略的线程池，Java 8 才加入这个创建方法，其内部会构建 [ForkJoinPool](https://docs.oracle.com/javase/9/docs/api/java/util/concurrent/ForkJoinPool.html) ,利用 [Work-Stealing](https://en.wikipedia.org/wiki/Work_stealing) 算法，并行地处理任务，不保证处理顺序。


11、线程池有什么好处？
>使用线程池管理线程资源，重复利用已创建的线程，避免了销毁线程时的开销，减少了创建新线程的次数与创建时的开销，而且这样一来相应的速度也将变得更快；此外还可以提高线程的可管理性；

12、cyclicbarrier和countdownlatch的区别
>CountdownLatch阻塞主线程，等所有子线程完结了再继续下去。Syslicbarrier阻塞一组线程，直至某个状态之后再全部同时执行，并且所有线程都被释放后，还能通过reset来重用。

13、如何理解Java多线程回调方法？
>* 回调：客户端请求服务器得到的回复中，包含执行客户端函数的信息，这个函数被称为回调函数，这个过程称为回调。回调的实现，可以是前后端工程师通过沟通约定好，也可以是前端在发送请求的时候带上回调的信息，告诉服务端进行回调；
>* 多线程回调：可以使对方线程(例如子线程)执行完毕后自动运行"回调方法"，而本线程(例如主线程)可以继续执行不必停下来等待。
>___
>[参考文章（原创版本的文章太难找了..）](https://blog.csdn.net/wenzhi20102321/article/details/52512536)


14、创建线程有几种不同的方式？你喜欢哪一种？为什么？
>* Thread
>* Runnable
>* Callable
>* Excutor

15、概括的解释下线程的几种可用状态。
>![状态之间的切换](https://upload-images.jianshu.io/upload_images/8463645-e1ef781e5074e029.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)关于线程生命周期的不同状态，在 Java 5 以后，线程状态被明确定义在其公共内部枚举类型 java.lang.Thread.State 中，分别是：
>* 新建（NEW），表示线程被创建出来还没真正启动的状态，可以认为它是个 Java 内部状态。
>* 就绪（RUNNABLE），表示该线程已经在 JVM 中执行，当然由于执行需要计算资源，它可能是正在运行，也可能还在等待系统分配给它 CPU 片段，在就绪队列里面排队。
>* 在其他一些分析中，会额外区分一种状态（RUNNING），但是从 Java API 的角度，并不能表示出来。
>* 阻塞（BLOCKED），这个状态和我们前面两讲介绍的同步非常相关，阻塞表示线程在等待 Monitor lock。比如，线程试图通过 synchronized 去获取某个锁，但是其他线程已经独占了，那么当前线程就会处于阻塞状态。
>* 等待（WAITING），表示正在等待其他线程采取某些操作。一个常见的场景是类似生产者消费者模式，发现任务条件尚未满足，就让当前消费者线程等待（wait），另外的生产者线程去准备任务数据，然后通过类似 notify 等动作，通知消费线程可以继续工作了。Thread.join() 也会令线程进入等待状态。
>* 计时等待（TIMED_WAIT），其进入条件和等待状态类似，但是调用的是存在超时条件的方法，比如 wait 或 join 等方法的指定超时版本，如下面示例：
>```
>public final native void wait(long timeout) throws InterruptedException;
>```
>* 终止（TERMINATED），不管是意外退出还是正常执行结束，线程已经完成使命，终止运行，也有人把这个状态叫作死亡（DEAD）。

16、同步方法和同步代码块的区别是什么？
>1\. 语法不同。 2. 同步块需要注明锁定对象，同步方法默认锁定this。 3. 在静态方法中，都是默认锁定类对象。 4. 在考虑性能方面，最好使用同步块来减少锁定范围提高并发效率。

17、启动线程有哪几种方式，线程池有哪几种？
>要启动的可以分为两类：返回结果和不返回结果。对于这两种，也分别有两种启动线程的方式：
1）继承Thread类，重载run()
2）实现Runnable接口，实现run()
3）实现Callable接口通过FutureTask包装器来创建Thread线程、使用ExecutorService、Callable、Future实现有返回结果的线程
>常用方法：
>1.newCachedThreadPool()
>2.newFixedThreadPool(int nThreads)
>3.newSingleThreadExecutor()
>4.newScheduleThreadPool()
>5.newWorkStealingPool(int parallelism)


18、在监视器(Monitor)内部，是如何做线程同步的？程序应该做哪种级别的同步？
>在 java 虚拟机中, 每个对象( Object 和 class )通过某种逻辑关联监视器,每个监视器和一个对象引用相关联, 为了实现监视器的互斥功能, 每个对象都关联着一把锁.
>
> java 提供了显式监视器( Lock )和隐式监视器( synchronized )两种锁方案，可以主动管理锁也可以交给JVM进行管理。
>
> 被synchronized修饰的代码 ，JVM会确保一次只能有一个线程执行被监听部分的代码, 线程在获取排他锁之前不允许执行该部分的代码

19、sleep() 和 wait() 有什么区别？
>1.sleep方法没有释放锁，但是wait方法释放了锁，使得其他线程可以使用同步控制块
2.sleep可以在任何地方使用，wait notify notifyall只能使用在同步控制块中
3.sleep必须捕获异常，其他不需要


20、同步和异步有何异同，在什么情况下分别使用他们？举例说明。
>* 同步：在同一时间不可以同时执行，步调必须按先后顺序一致（同步词汇的由来）；
>* 异步：在同一时间可以同时执行，步调可以不按先后顺序一致（异步词汇的由来）；
> 
>使用策略：所有非原子的写操作，都理应同步执行，如果异步，则会可能破坏数据的一致性（与事实的一致性）；
>举例：银行结算系统，有100个人几乎同时向某用户转账10元钱，此时，如果异步执行，在CPU切换线程的时候就很容易出现记账错误的问题（有某些线程的执行效果被另外的线程低效掉了）；而同步执行不会出现这样的问题；若想提升性能，可以将同步的粒度缩小至具体修改数据的那一步；

21、设计4个线程，其中两个线程每次对j增加1，另外两个线程对j每次减少1。使用内部类实现线程，对j增减的时候没有考虑顺序问题。
>```
>/**
>*使用时，创建此类的实例，并将得到的实例对象传给线程，
>*在线程里调用change()即可实现目的
>*/
>class Data{
>    
>    public int j = 0;  // 存放j的值，支持外部修改（改为合适的初始值）
>    
>    public void synchronized change(boolean isAdd){
>        try{
>            synchronized(j){  // 定义同步代码块
>                if(isAdd){
>                     j++;
>                }else{
>                     j--;
>                }
>            }catch(Exception e){
>                e.printStackTrace();
>            }
>        }     
>    }
>
>}
>```
>此外，还可以选择使用原子类来存放 j 的值
>___
>[参考文章：synchronized同步代码块语法示例与说明](https://blog.csdn.net/qq_26545305/article/details/79135967)

22、启动一个线程是用run()还是start()?
>start()

23、请说出你所知道的线程同步的方法
>synchronized、Lock、原子类

24、多线程有几种实现方法,都是什么?同步有几种实现方法,都是什么?
>* 多线程的实现方法：
1）继承Thread类，重载run()
2）实现Runnable接口，实现run()
3）实现Callable接口
>* 同步的实现方法：
1）synchronized —— 同步方法 or 同步代码块
2）使用 Lock 的实现类主动管理资源锁
3）使用原子类来存放数据

25、java中有几种方法可以实现一个线程？用什么关键字修饰同步方法? stop()和suspend()方法为何不推荐使用？
>线程的实现方法：
1）继承Thread类，重载run()
2）实现Runnable接口，实现run()
3）实现Callable接口
>
>synchronized 
>
>* stop()：强制停止线程，释放锁；由于不管run有没有结束都会停止，容易造成数据不一致，例如银行转账；1.2后被弃用
>* suspend()：暂停执行，且不释放资源；很容易造成死锁，例如一直没有resume，1.2后被弃用

26、线程的sleep()方法和yield()方法有什么区别？
>![我整理的线程调度方法](https://upload-images.jianshu.io/upload_images/8463645-a5e5ffb8aeb85d14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



27、当一个线程进入一个对象的synchronized方法A之后，其它线程是否可进入此对象的synchronized方法B？
>* 如果是非静态方法，则不能，因为非静态方法是基于实例 this 的；（而每个对象只有一个锁监听器，是这个原因吗？）
>* 如果是静态方法，则可以，因为静态方法不需要依赖对象，与具体非静态方法是互不影响的；如果静态方法被 synchronized 修饰，则会将其所在类给锁住；

28、请说出与线程同步以及线程调度相关的方法。
>见前面26.

29、举例说明同步和异步
>* 同步：在同一时间不可以同时执行，步调必须按先后顺序一致（同步词汇的由来）；
>* 异步：在同一时间可以同时执行，步调可以不按先后顺序一致（异步词汇的由来）；

30、什么是线程池（thread pool）？
>线程池是存储线程的容器,线程事先创建好后放入线程池,当有任务需要执行时,直接从线程池拿空闲线程使用,使用完毕后归还给线程池.
>
>使用线程池的几点好处:
>1.可以节省创建线程和销毁线程需要的系统资源;（线程使用完毕后不会立即被销毁，而是管理起来、重复利用）
>2.可以提高响应的速度,减少用户等待时间;（因为不需要再重新创建线程了）
>3.通过控制线程池的大小,可以增强系统的可控性.


31、说说线程的基本状态以及状态之间的关系？
>详细文字描述可见本小节前面的 问题15.![状态之间的切换](https://upload-images.jianshu.io/upload_images/8463645-e1ef781e5074e029.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


32、如何保证线程安全？
>synchronized、Lock、原子类

#### **❤6、锁**

1、讲一下非公平锁和公平锁在reetrantlock里的实现。
>* 公平锁与非公平锁：可以说是操作系统提到的关于任务调度"公平性"的体现，公平性指等待越久的线程越容易也越应该拿到锁资源（例如按请求顺序获得锁的FIFO），这样可以确保每个线程都有稳定的机会拿到锁资源，而非公平性则是指线程能不能拿到锁与等待时间无关（允许插队），每个线程拿到锁的机会没有保障，容易产生饥饿甚至饿死现象；
>* Reetrantlock 的实现：（1）（2）

2、讲一下synchronized，可重入怎么实现。
>* 可重入：有这样一个方法，首先它的有锁的，需要持有该锁才能调用它，而如果它又调用它自身的话，如果锁是可重入的则可以调用不需要再去申请获取锁(如果申请是申请不到的)，如果是不可重入的，则无法调用自身，形成死锁。我认为可以这样简单理解：在自身的调用权限加锁的情况下，是否允许自己调用自己。
>* AQS：![来自牛客网的资料](https://upload-images.jianshu.io/upload_images/8463645-d35fe40c0577d17f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>* CAS：当且仅当V==A时，执行D=B，否则自旋重新获取D的值重新计算B；（D:数据变量，V:当前线程读取到的用于计算存于内存的D值，A:当要修改D值之前再次读取的用于与V比较检验D是否还是原值的比较数据，B:当前线程计算完毕准备修改进D里的值）【jdk1.8更新的基本数据类型原子类的原子操作底层都是用CAS和自旋锁实现的】
>* synchronized可重入性的实现：每个锁关联一个线程持有者和一个计数器。当计数器为0时表示该锁没有被任何线程持有，那么任何线程都都可能获得该锁而调用相应方法。当一个线程请求成功后，JVM会记下持有锁的线程，并将计数器计为1。此时其他线程请求该锁，则必须等待。而该持有锁的线程如果再次请求这个锁，就可以再次拿到这个锁，同时计数器会递增。当线程退出一个synchronized方法/块时，计数器会递减，如果计数器为0则释放该锁。
>___
>[参考资料：Java里15种锁的介绍](https://my.oschina.net/u/3954808/blog/3062294)
>[参考资料：JavaAQS无码讲解](https://zhuanlan.zhihu.com/p/49326706)
>[牛客网题目：请你说一下AQS](https://www.nowcoder.com/ta/review-test/review?page=110)
>[参考资料：Java多线程synchronized的可重入性](https://www.cnblogs.com/cielosun/p/6684775.html)


3、锁和同步的区别。
>* 锁：限制资源的访问权限
>* 同步：在同一时间不可以同时执行，步调必须按先后顺序一致（同步词汇的由来）；
>* 异步：在同一时间可以同时执行，步调可以不按先后顺序一致（异步词汇的由来）；


4、什么是死锁(deadlock)？
>* 一句话描述：若干线程相互循环等待对方已占有的资源。
>* 死锁的必要条件：
>1）互斥：一个资源每次只能被一个线程使用
>2）请求与保持：一个线程因请求资源而阻塞时，对已获得的资源保持不放
>3）不剥夺：线程已获得的资源，在末使用完之前，其他线程不能强行剥夺
>4）循环等待：若干进程之间形成一种头尾相接的循环等待对方已占有资源的关系


5、如何确保N个线程可以访问N个资源同时又不导致死锁？
>破坏死锁产生的必要条件；使用合适的调度算法，例如银行家算法。
>___
>* 银行家算法：
>1\. 重要前提假设：线程在获取够所有所需资源之前，不会完成工作内容结束运行并归还已经获取到的资源；（银行的客户必须借到工程项目所需的所有资金才能够完成项目并还钱）
2\. 当有多个线程同时申请资源时（有多个客户同时向银行借钱，这些客户可能以前已经借过一些钱，尚未归还），在分配资源给进程之前（借钱给客户之前），先对自己资源的健康程度进行预分配检验，检验资源分配给某个线程之后（借钱给某客户），自己现有的剩余资源，和已分配出有很大把握可以拿回来的资源（资金），是否还有足够继续满足剩余的其他线程（客户）；如果安全，则分配，否则，不进行资源分配；

6、请你简述synchronized和java.util.concurrent.locks.Lock的异同？
>* Lock：粒度更小，可以读写锁分离，性能略优；
>* synchronized：代码编写便捷，性能会略差一点；

#### **❤7、JDK**

1、Java中的LongAdder和AtomicLong的区别
>* AtomicLong：Long类型的线程安全原子类；
>* LongAdder：在低竞争的情况下性能与 AtomicLong 相近，在高竞争的清空下性能远优于 AtomicLong；
>___
>[参考文章：AtomicLong与LongAdder性能对比](https://zhuanlan.zhihu.com/p/45489739)


2、JDK和JRE的区别是什么？
>作者：王博
链接：https://www.zhihu.com/question/20317448/answer/14737358
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
>
>JRE： Java Runtime Environment
JDK：Java Development Kit
JRE顾名思义是java运行时环境，包含了java虚拟机，java基础类库。是使用java语言编写的程序运行所需要的软件环境，是提供给想运行java程序的用户使用的。
JDK顾名思义是java开发工具包，是程序员使用java语言编写java程序所需的开发工具包，是提供给程序员使用的。JDK包含了JRE，同时还包含了编译java源码的编译器javac，还包含了很多java程序调试和分析的工具：jconsole，jvisualvm等工具软件，还包含了java程序编写所需的文档和demo例子程序。
如果你需要运行java程序，只需安装JRE就可以了。如果你需要编写java程序，需要安装JDK。
JRE根据不同操作系统（如：windows，linux等）和不同JRE提供商（IBM,ORACLE等）有很多版本，最常用的是Oracle公司收购SUN公司的JRE版本。如果你想查看更官方的解释，可以前往Oracle官网：[http://www.oracle.com/cn/technologies/java/overview/index.html](https://link.zhihu.com/?target=http%3A//www.oracle.com/cn/technologies/java/overview/index.html)


#### **❤8、反射**

1、反射的实现与作用
>* 实现：
>* 作用：可以在运行的时候再加载类信息（可以获取类里面的方法、字段信息，用于自动化参数打印/传输），也可以用来使用抽象设计模式（例如抽象工厂设计模式的基于反射的）；
>___
>[参考文章：JAVA反射机制的作用是什么](https://cloud.tencent.com/developer/article/1344254)

#### **😀9、JVM**

1、JVM回收算法和回收器，CMS采用哪种回收算法，怎么解决内存碎片问题？
>* 7大收集器：Serial/Serial Old、ParNew、Parallel Scavenge（Parallel Young）/Parallel Old、CMS、G1![七大GC收集器](https://upload-images.jianshu.io/upload_images/8463645-c3a2a2ac786f92d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>* 默认收集器：ParallelGC收集器，即 Parallel Scavenge（Parallel Young）+ Parallel Old
>* CMS采用Mark-Sweep标记清除法（Concurrent Mark Sweep，顾名思义），是老年代的收集器，会产生较多内存碎片，当老年代没有足够的连续内容容纳新生代晋升的数据时，会导致FullGC，[网上搜到的解决办法有](https://www.cnblogs.com/tiancai/p/9359939.html)：
> 1\. 增大Xmx或者减少Xmn
> 2\. 在应用访问量最低的时候，在程序中主动调用System.gc()，比如每天凌晨。
> 3\. 在应用启动并完成所有初始化工作后，主动调用System.gc()，它可以将初始化的数据压缩到一个单独的chunk中，以腾出更多的连续内存空间给新生代晋升使用。
> 4\. 降低-XX:CMSInitiatingOccupancyFraction参数以提早执行CMSGC动作，虽然CMSGC不会进行内存碎片的压缩整理，但它会合并老生代中相邻的free空间。这样就可以容纳更多的新生代晋升行为。
>___
>*深入探究GC需要很多时间，也比较需要结合实际的瓶颈案例才能掌握得更牢固深刻，大多数公司校招时不会问得很深。但是如果将GC掌握得非常到位，绝对会非常非常脱颖而出。*


2、类加载过程
>当代码逻辑使用涉及到某个类时(具体形式可以是new也可以是反射)，会通过类加载机制的流程加载这个类，流程：
>* 加载：默认由"双亲委派机制"(父类加载器委派)通过有能力加载的最高层次加载器加载类的class文件
>* 链接：将Java类的二进制代码合并到JVM的运行状态之中，具体包括：
>1）验证：确保加载的类信息符合JVM规范，没有安全方面的问题
>2）准备：正式为类变量(static变量)分配内存并设置类变量初始值的阶段，这些内存都将在方法区中进行分配。注意此时的设置初始值为默认值，具体赋值在初始化阶段完成。
>3）解析：虚拟机常量池内的符号引用替换为直接引用（地址引用）的过程。
>* 初始化：给静态内容赋予实际的初始值，顺序是先父后子，先完成父子的所有静态变量再构造方法
>___
>*能答出这些，可以认为你是对jvm类加载有一定了解的，如果面试人数多面试官比较赶时间的话可能不会再深究细节，但是也要做好准备，一些大公司的面试还是非常有可能会深挖下去的，能挖多深挖多深。*

3、JVM分区
>* 堆：是所有对象实际数据的存放位置，被所有线程共享，里面又分为 Eden 和 Survial 即新生代老年代。
>* 虚拟机栈：VM Stack，也就是我们所说的栈内存，是java方法执行的内存模型。每个方法在执行的时候都会创建一个栈帧，用于存储局部变量表、操作数栈、动态链接、和方法返回地址等信息。
>* 本地方法栈：与VM Stack类型，不过这里是本地方法（native）的专用内存栈。
>* 方法区：区别于堆存放对象数据内容，方法区主要负责存放静态变量、常量、静态方法等信息。由于这里存在一些性能低的瓶颈以及比较死板的固定默认大小，JDK1.7和JDK1.8对此均有较大改动。
>* 程序计数器：记录即将要执行的指令所在的行数，每个线程都需要有自己独立的程序计数器，并且不能互相被干扰。
>___
>[参考文章1：JVM五大分区](https://blog.csdn.net/qq_32755757/article/details/85259133)
>[参考文章2：Java内存区域介绍（附带JDK1.8后方法区的变化）](https://blog.csdn.net/weixin_42762133/article/details/95735737)
>[参考文章3：JDK 1.8 JVM的变化](https://www.cnblogs.com/yangyongjie/p/10646255.html)

4、eden区，survial区?
>* eden区：一些有效时间比较临时短暂的对象适合存放的内存区域（堆内），它里面还包含两个轮流存放数据内容的采用了Copying垃圾收集思想的临时晋升过渡观察区；
>* survial区：一些有效时间比较稳定长久的对象适合存放的内存区域（堆内），里面的对象由 eden 区通过GC淘汰机制晋升而来；
>* 分区的目的是为了针对不同的业务场景，采用不同的GC策略，更高效稳定地管理有限的内存资源；

5、JAVA虚拟机的作用?
>封装并管理不同设备环境的内存资源，为Java代码提供一个统一的直接运行环境，达到“compile once, run anywhere”的效果。

6、GC中如何判断对象需要被回收？
>* 引用计数法：记录被引用的次数。这样做，若出现"循环依赖"，则会导致内存泄露。
>* 可达性分析法：判断对象的引用链是否可达 GC Roots：![我整理的](https://upload-images.jianshu.io/upload_images/8463645-d0ca9a4873c43e92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


7、JAVA虚拟机中，哪些可作为ROOT对象？
>可以将这些看作Root对象：![我整理的](https://upload-images.jianshu.io/upload_images/8463645-d0ca9a4873c43e92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8、JVM内存模型是什么？
>JMM(Java Memory Model) 是线程间通信的机制 。线程间共享变量存储在主内存，每个线程都有自己的本地内存，存储的是共享变量在本地的副本
>* 主内存（内存）
>* 线程内存（CPU缓存）

9、jvm是如何实现线程？
>* Java语言的线程操作略，见前文的内容。
>* JVM底层是通过程序计数器来实现多线程的：每一个线程都会单独开辟一块内存区域给程序计数器，线程之间这块内存区域是隔离的，是安全的；于是多线程在调度切换的时候可以继续执行上次挂起时的下一条指令。
>___
>[牛客网友回答](https://www.nowcoder.com/questionTerminal/1a380049569c43d2b238b69bbd17dc9e?orderByHotValue=1&page=1&onlyReference=false)：java代码通过Thread类或者Runnable，调用其start方法后创建一个线程。其本质是jvm通过调用Thread.cpp中本地方法pthread_create创建新线程，创建线程的同时在jvm中为线程分配内存空间，即为其分配一个私有的程序计数器、虚拟机栈和本地方法栈。创建线程的方式有三种：用户线程、轻量级进程和内核线程，java线程是基于操作系统原生的线程模型


10、jvm最大内存限制多少
>机器物理内存 > JVM可用总内存 > 连续空闲可用内存
>关于不同的操作系统有这样一种[说法](https://www.nowcoder.com/questionTerminal/855006adab6b45afb9fe98e3c72b90d6?orderByHotValue=1&page=1&onlyReference=false)（未考证）：
>* 对于32位操作系统，可控内存空间有4GB,但是具体的操作系统会给一个限制，这个限制一般是2GB-3GB（一般来说Windows系统下为1.5G-2G，Linux系统 下为2G-3G）
>* 对于64位操作系统，不会有限制

11、什么是Java虚拟机？为什么Java被称作是“平台无关的编程语言”？
>JVM是一种封装了设备资源的可供Java代码运行使用的环境（通过封装调用不同平台环境的资源访问接口）；
>不同的平台环境有不同类型的JVM，而JVM处理的是同样的Java代码编译生成的 .class 文件，于是Java代码的运行就与平台无关了。
>___
>![文章里的图片](https://upload-images.jianshu.io/upload_images/8463645-7bc01c566a0ef9eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
[辅助理解的一篇文章](https://www.cnblogs.com/alilcu/p/8068508.html)


12、描述一下JVM加载class文件的原理机制?
>加载方式：1.隐式装载， 程序在运行过程中当碰到通过new 等方式生成对象时，隐式调用类装载器加载对应的类到jvm中，2.显式装载， 通过class.forname()等方法，显式加载需要的类。流程：
>* 加载：默认由"双亲委派机制"(父类加载器委派)通过有能力加载的最高层次加载器加载类的class文件
>* 链接：将Java类的二进制代码合并到JVM的运行状态之中，具体包括：
>1）验证：确保加载的类信息符合JVM规范，没有安全方面的问题
>2）准备：正式为类变量(static变量)分配内存并设置类变量初始值的阶段，这些内存都将在方法区中进行分配。注意此时的设置初始值为默认值，具体赋值在初始化阶段完成。
>3）解析：虚拟机常量池内的符号引用替换为直接引用（地址引用）的过程。
>* 初始化：给静态内容赋予实际的初始值，顺序是先父后子，先完成父子的所有静态变量再构造方法

#### **❤10、GC**

1、java中内存泄露是啥，什么时候出现内存泄露？
>* 内存泄露：已经使用完毕的内存无法被回收，一直占用着资源，变相地使一部分内存变得"不可用"，于是被称为"内存泄露"；
>* Java容易出现内存泄露的常见情景：
>（1）不妥当地使用单例模式：例如生存周期长的对象(单例对象)引用了另一个生存周期短的对象，那么那个生存周期短的对象将不会被回收；
>（2）不妥当地使用公用的静态集合：例如只写了添加内容的代码，未写删除内容的代码；
>（3）总的来说就是，创建任何对象时都应该考虑它的销毁是否会自动发生，若不会则记得要自行管理它的销毁；


2、minor gc如果运行的很频繁，可能是什么原因引起的，minor gc如果运行的很慢，可能是什么原因引起的?
>* 频率高的原因：太多生存周期短的对象引发的GC回收；新生代的空间设置过小；
>* 速度慢的原因：新生代的空间设置过大；对象引用链较长，进行可达性分析时间较长；survivor区设置过小，容纳不下所有幸存者，引发了对象移动到老年代的开销；
>___
>[参考文章：牛客网同名问题的回答](https://www.nowcoder.com/questionTerminal/b3cd86f89d6c4b1ab54252b49a6bff57)


3、阐述GC算法
> GC算法是为了更好地管理计算机设备资源，为Java程序提供更好的运行环境JVM而设计的一系列内存管理算法；思路有以下这些：
>* 标记清除
>* 标记-整理-清除
>* 复制
>* 分代收集

4、GC是什么? 为什么要有GC?
> 同上问题3.

5、垃圾回收的优点和原理。并考虑2种回收机制
> * 优点：为JVM管理计算机内存资源，使Java程序能够有更好的、资源更充裕运行环境；
> * 原理：内存管理方法的多种具体实现；
> * 回收机制：G1、CMS

6、java中会存在内存泄漏吗，请简单描述。
> 会的。例如未妥当地管理静态对象的内容；详见上问题1.

7、垃圾回收器的基本原理是什么？垃圾回收器可以马上回收内存吗？有什么办法主动通知虚拟机进行垃圾回收？（垃圾回收）
> 主动通知JVM进行GC的方法：System.gc()

#### **❤11、IO和NIO、AIO**

1、怎么打印日志？

2、运行时异常与一般异常有何异同？

3、error和exception有什么区别?

4、给我一个你最常见到的runtime exception

5、Java中的异常处理机制的简单原理和应用。

6、java中有几种类型的流？JDK为每种类型的流提供了一些抽象类以供继承，请说出他们分别是哪些类？

7、什么是java序列化，如何实现java序列化？
> * 序列化这里指的是将Java对象按照特定的格式，将内容转化为字符串，生成的字符串往往是序列化存储的，查找时非常方便，故也将此过程称为Java序列化。

8、运行时异常与受检异常有什么区别？

### 二、JavaEE部分

#### **❤1、Spring**

1、说一下IOC和AOP?

2、介绍一下bean的生命周期
> * Bean是什么：(我的理解) bean是一种特殊的对象，相比于OOP编程时创建的真实创建并存储到计算机内存里的对象（例如POJO，Plain Ordinary Java Object，可以理解为功能明确的高内聚Java对象），bean是从抽象角度理解的对象，可以理解为POJO是bean的具体内容；
> * EJB容器：是一种封装了业务并对外提供调用接口的特殊bean容器，它的作用可以理解为两点：1."发生在服务端的C/S"、2."通过RPC调用，使应用可以分布式部署"。因为它非常适合用于构建企业级中大型应用，于是被称为Enterprise JavaBean。![EJB配图](https://upload-images.jianshu.io/upload_images/8463645-1258a0a95a839dd0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)*（EJB的历史笔者没有深究，笔者仅基于自己对EJB粗略的了解猜测：由于它有上面提到的亮点好处，似乎EJB是在Spring流行之前的上一代容器弄潮者，但由于它存在一些性能问题，冗余较多，被后来的轻量级容器Spring给比下去了）*
>
> * Bean容器 Spring：bean的一种管理工具
> * Spring Bean生命周期：
>___
>EJB解释文章：[文章一](https://blog.csdn.net/jojo52013145/article/details/5783677)、[文章二](https://www.cnblogs.com/EasonJim/p/7103546.html)
>SpringBeen文章：[Spring Bean scope种类](http://www.voidcn.com/article/p-hmnqntnl-xp.html)




3、Spring里面注解用过没有？autowired 和resource区别？

4、@Controller和@RestController的区别？

5、依赖注入的方式有几种，哪几种？

6、springIOC原理？自己实现IOC要怎么做，哪些步骤？

7、Spring中BeanFactory和ApplicationContext的区别？、

8、什么是IoC和DI？DI是如何实现的？

9、请问Spring中Bean的作用域有哪些？

10、谈谈Spring中自动装配的方式有哪些？

11、aop的应用场景？

12、AOP的原理是什么？

13、你如何理解AOP中的连接点（Joinpoint）、切点（Pointcut）、增强（Advice）、引介（Introduction）、织入（Weaving）、切面（Aspect）这些概念？

14、Spring支持的事务管理类型有哪些？你在项目中使用哪种方式？

15、介绍一下spring？

16、Struts拦截器和Spring AOP区别？

17、spring框架的优点？

18、选择使用Spring框架的原因（Spring框架为企业级开发带来的好处有哪些）？

19、持久层设计要考虑的问题有哪些？你用过的持久层框架有哪些？

#### **❤2、Hibernate**

没学 Hibernate，搜资料大概了解到它的优缺点如下：
优点

缺点

1、阐述实体对象的三种状态以及转换关系。

2、Hibernate中SessionFactory是线程安全的吗？Session是线程安全的吗（两个线程能够共享同一个Session吗）？

3、Hibernate中Session的load和get方法的区别是什么？

4、如何理解Hibernate的延迟加载机制？在实际应用中，延迟加载与Session关闭的矛盾是如何处理的？

4、简述Hibernate常见优化策略。

5、锁机制有什么用？简述Hibernate的悲观锁和乐观锁机制。

6、Hibernate如何实现分页查询？

7、谈一谈Hibernate的一级缓存、二级缓存和查询缓存。

#### **❤3、Struts**

1、说说STRUTS的应用

#### **❤4、Mybatis**

1、解释一下MyBatis中命名空间（namespace）的作用。

2、MyBatis中的动态SQL是什么意思？

#### **❤5、MVC**

1、Spring MVC注解的优点

2、springmvc和spring-boot区别？

3、SpringMVC的运行机制，运行机制的每一部分的相关知识？

4、谈谈Spring MVC的工作原理是怎样的？

#### **❤6、各框架对比与项目优化**

1、Mybatis和Hibernate区别？

2、介绍一下你了解的Java领域的Web Service框架。

#### **❤7、JPA**

1、EJB是基于哪些技术实现的？并说出SessionBean和EntityBean的区别，StatefulBean和StatelessBean的区别。

2、EJB与JAVA BEAN的区别？

3、EJB包括（SessionBean,EntityBean）说出他们的生命周期，及如何管理事务的？

4、EJB的角色和三个对象是什么？

5、说说EJB规范规定EJB中禁止的操作有哪些？

6、EJB的激活机制是什么？

7、EJB的几种类型分别是什么

8、EJB需直接实现它的业务接口或Home接口吗，请简述理由。

### 三、Java  web编程

#### **❤1、web编程基础**

1、启动项目时如何实现不在链接里输入项目名就能启动?

2、1分钟之内只能处理1000个请求，你怎么实现，手撕代码?

3、什么时候用assert

4、JAVA应用服务器有那些？

5、JSP的内置对象及方法。

6、JSP和Servlet有哪些相同点和不同点，他们之间的联系是什么？（JSP）

7、说一说四种会话跟踪技术

8、讲讲Request对象的主要方法

9、说说weblogic中一个Domain的缺省目录结构?比如要将一个简单的helloWorld.jsp放入何目录下,然后在浏览器上就可打入主机？

10、jsp有哪些动作?作用分别是什么?

11、请谈谈JSP有哪些内置对象？作用分别是什么？

12、说一下表达式语言（EL）的隐式对象及其作用

13、JSP中的静态包含和动态包含有什么区别？

14、过滤器有哪些作用和用法？

15、请谈谈你对Javaweb开发中的监听器的理解？

16、说说web.xml文件中可以配置哪些内容？

#### **❤2、web编程进阶**

1、forward与redirect区别，说一下你知道的状态码，redirect的状态码是多少？

2、servlet生命周期，是否单例，为什么是单例。

3、说出Servlet的生命周期，并说出Servlet和CGI的区别。

4、Servlet执行时一般实现哪几个方法？

5、阐述一下阐述Servlet和CGI的区别?

6、说说Servlet接口中有哪些方法？

7、Servlet 3中的异步处理指的是什么？

8、如何在基于Java的Web项目中实现文件上传和下载？

9、服务器收到用户提交的表单数据，到底是调用Servlet的doGet()还是doPost()方法？

10、Servlet中如何获取用户提交的查询参数或表单数据？

11、Servlet中如何获取用户配置的初始化参数以及服务器上下文参数？

12、讲一下redis的主从复制怎么做的？

13、redis为什么读写速率快性能好？

14、redis为什么是单线程？

15、缓存的优点？

16、aof，rdb，优点，区别？

17、redis的List能用做什么场景？

18、说说MVC的各个部分都有那些技术来实现?如何实现?

19、什么是DAO模式？

20、请问Java Web开发的Model 1和Model 2分别指的是什么？

21、你的项目中使用过哪些JSTL标签？

22、使用标签库有什么好处？如何自定义JSP标签？（JSP标签）

#### **❤3、web编程原理**

1、get和post区别？
>get在url里传输参数，有大小限制，容易泄露信息；post在请求体里传输参数，无大小限制，不容易泄露信息；

2、请谈谈转发和重定向的区别？
>

3、说说你对get和post请求，并且说说它们之间的区别？

4、cookie 和session 的区别？
>

5、forward 和redirect的区别
>

6、BS与CS的联系与区别。
>B指浏览器，C指客户端

7、如何设置请求的编码以及响应内容的类型？
>

8、什么是Web Service（Web服务）？
>

9、谈谈Session的save()、update()、merge()、lock()、saveOrUpdate()和persist()方法分别是做什么的？有什么区别？
>

10、大型网站在架构上应当考虑哪些问题？
>高内聚、低耦合，减少冗余代码，巧用设计模式

11、请对J2EE中常用的名词进行解释(或简单描述)
>

### 四、JDBC编程

#### **❤1、SQL基础**

1、写SQL：找出每个城市的最新一条记录。

2、一个学生表，一个课程成绩表，怎么找出学生课程的最高分数

3、有一组合索引（A,B,C），会出现哪几种查询方式？tag:sql语句

#### **❤2、JDBC基础**

1、数据库水平切分，垂直切分
>

2、数据库索引介绍一下。介绍一下什么时候用Innodb什么时候用MyISAM。
>

3、数据库两种引擎
>

4、索引了解嘛，底层怎么实现的，什么时候会失效
>

5、问了数据库的隔离级别
>

6、数据库乐观锁和悲观锁
>

7、数据库的三范式？
>

8、讲一下数据库ACID的特性？
>

9、mysql主从复制？
>

10、leftjoin和rightjoin的区别？
>

11、数据库优化方法
>

12、谈一下你对继承映射的理解。
>

13、说出数据连接池的工作机制是什么?
>

14、事务的ACID是指什么？
>

15、JDBC中如何进行事务处理？
>

#### **❤3、JDBC进阶**

1、JDBC的反射，反射都是什么？
>

2、Jdo是什么?
>

3、Statement和PreparedStatement有什么区别？哪个性能更好？
>

4、使用JDBC操作数据库时，如何提升读取数据的性能？如何提升更新数据的性能？
>

### 五、XML

#### **❤1、XML基础**

1、XML文档定义有几种形式？它们之间有何本质区别？解析XML文档有哪几种方式？
>

#### **❤2、Web Service**

1、WEB SERVICE名词解释，JSWDL开发包的介绍，JAXP、JAXM的解释。SOAP、UDDI,WSDL解释。

2、请你谈谈对SOAP、WSDL、UDDI的了解？

3、谈谈Java规范中和Web Service相关的规范有哪些？

### 六、计算机网络

#### **❤1、网络概述**

1、TCP协议在哪一层？IP协议在那一层？HTTP在哪一层？

#### **❤2、运输层**

1、讲一下TCP的连接和释放连接。

2、TCP有哪些应用场景

3、tcp为什么可靠

4、tcp为什么要建立连接

5、阐述TCP的4次挥手

6、讲一下浏览器从接收到一个URL到最后展示出页面，经历了哪些过程。tag

7、http和https的区别

8、http的请求有哪些，应答码502和504有什么区别

9、http1.1和1.0的区别

10、说说ssl四次握手的过程

11、304状态码有什么含义？

#### **❤3、网络层**

1、arp协议，arp攻击

2、icmp协议

3、讲一下路由器和交换机的区别？

#### **❤4、应用层**

1、DNS寻址过程

2、负载均衡反向代理模式优点及缺点

### 七、操作系统

#### **❤1、操作系统概论**

1、CentOS 和 Linux的关系？

2、64位和32位的区别？

#### **❤2、进程的描述与控制**

1、怎么杀死进程？

2、线程，进程区别

3、系统线程数量上限是多少？

4、进程和线程的区别是什么？

5、解释一下LINUX下线程，GDI类。

#### **❤3、输入输出系统**

1、socket编程，BIO，NIO，epoll？

#### **❤4、存储器管理**

1、什么是页式存储？

2、操作系统里的内存碎片你怎么理解，有什么解决办法？

#### **❤5、处理机调度与死锁**

1、什么情况下会发生死锁，解决策略有哪些？

2、系统CPU比较高是什么原因？

3、系统如何提高并发性？

### 八、算法与数据结构

#### **❤1、哈希**

1、hashset存的数是有序的吗？

2、Object作为HashMap的key的话，对Object有什么要求吗？

3、一致性哈希算法

4、什么是hashmap?

5、Java中的HashMap的工作原理是什么？

6、hashCode()和equals()方法的重要性体现在什么地方？

#### **❤2、树**

1、说一下B+树和B-树？

2、怎么求一个二叉树的深度?手撕代码?

3、算法题：二叉树层序遍历，进一步提问：要求每层打印出一个换行符

4、二叉树任意两个节点之间路径的最大长度

5、如何实现二叉树的深度？

6、如何打印二叉树每层的节点？

7、TreeMap和TreeSet在排序时如何比较元素？Collections工具类中的sort()方法如何比较元素？

#### **❤3、遍历**

1、编程题：写一个函数，找到一个文件夹下所有文件，包括子文件夹

2、二叉树 Z 字型遍历

#### **❤4、链表**

1、反转单链表

2、随机链表的复制

3、链表-奇数位升序偶数位降序-让链表变成升序

4、bucket如果用链表存储，它的缺点是什么？

5、如何判断链表检测环

#### **❤5、数组**

1、寻找一数组中前K个最大的数

2、求一个数组中连续子向量的最大和

3、找出数组中和为S的一对组合，找出一组就行

4、一个数组，除一个元素外其它都是两两相等，求那个元素?

5、算法题：将一个二维数组顺时针旋转90度，说一下思路。

#### **❤6、排序**

1、排序算法知道哪些，时间复杂度是多少，解释一下快排？

2、如何得到一个数据流中的中位数？

3、堆排序的原理是什么？

4、归并排序的原理是什么？

5、排序都有哪几种方法？请列举出来。

6、如何用java写一个冒泡排序？

#### **❤7、堆与栈**

1、堆与栈的不同是什么？

2、heap和stack有什么区别。

3、解释内存中的栈(stack)、堆(heap)和静态区(static area)的用法。

#### **❤8、队列**

1、什么是Java优先级队列(Priority Queue)？

#### **❤9、高级算法**

1、题目：

Design and implement a data structure for Least Frequently Used (LFU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.

put(key, value) - Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For the purpose of this problem, when there is a tie (i.e., two or more keys that have the same frequency), the least recently used key would be evicted.

Could you do both operations in O(1) time complexity?

2、id全局唯一且自增，如何实现？

3、如何设计算法压缩一段URL？

4、为什么要设计后缀表达式，有什么好处？

5、LRU算法的实现原理？

### 九、设计模式

#### **❤1、结构型模式**

1、java中有哪些代理模式？

2、如何实现动态代理

3、IO流熟悉吗，用的什么设计模式？

#### **❤2、创建型模式**

1、介绍一下单例模式？懒汉式的单例模式如何实现单例？

#### **❤3、行为型模式**

1、介绍一下策略模式？

2、设计模式了解哪些，手写一下观察者模式？

#### **❤4、模式汇总**

1、说说你所熟悉或听说过的j2ee中的几种常用模式?及对设计模式的一些看法

2、j2ee常用的设计模式？说明工厂模式。

3、开发中都用到了那些设计模式?用在什么场合?

4、简述一下你了解的Java设计模式

### 十、场景题

#### **❤1、场景题汇总**

1、情景题：如果一个外卖配送单子要发布，现在有200个骑手都想要接这一单，如何保证只有一个骑手接到单子？
2、场景题：美团首页每天会从10000个商家里面推荐50个商家置顶，每个商家有一个权值，你如何来推荐？第二天怎么更新推荐的商家？
可以借鉴下stackoverflow，视频网站等等的推荐算法。
3、场景题：微信抢红包问题
悲观锁，乐观锁，存储过程放在mysql数据库中。
4、场景题：1000个任务，分给10个人做，你怎么分配，先在纸上写个最简单的版本，然后优化。
全局队列，把1000任务放在一个队列里面，然后每个人都是取，完成任务。
分为10个队列，每个人分别到自己对应的队列中去取务。
5、场景题：保证发送消息的有序性，消息处理的有序性。
6、如何把一个文件快速下发到100w个服务器
7、给每个组分配不同的IP段，怎么设计一种结构使的快速得知IP是哪个组的?
8、10亿个数，找出最大的10个。
建议一个大小为10的小根堆。
9、有几台机器存储着几亿淘宝搜索日志，你只有一台2g的电脑，怎么选出搜索热度最高的十个搜索关键词？
10、分布式集群中如何保证线程安全？
11、给个淘宝场景，怎么设计一消息队列？
12、10万个数，输出从小到大？
先划分成多个小文件，送进内存排序，然后再采用多路归并排序。
13、有十万个单词，找出重复次数最高十个？

### 十一、UML

#### **❤1、UML**

1、请你谈一下UML中有哪些常用的图？

## 【三、其他考点】
1.  哪些排序算法是稳定的？哪些是不稳定的？
>稳定：冒泡、插入、归并、基数（冒插基归 桶计）、桶排序、计数排序
不稳定：交换、选择、希尔、快速、堆（希选交快堆）

2. 对比 Vector、ArrayList、LinkedList 有何区别？
>这三者都是实现集合框架中的List，也就是所谓的有序集合，因此具体功能也比较近似，都提供按照位置进行定位、添加或者删除的操作，都提供迭代器以遍历其内容等。但因为具体的设计区别，在行为、性能、线程安全方面，表现又有很大不同。
>
>Vector是Java早期提供的线程安全的动态数组，如果不需要线程安全，并不建议选择，毕竟同步是有额外开销的。Vector内部是使用对象数组来保存数据，可以根据需要自动的增加容量，当数组已满时，会创建新的数组，并拷贝原有的数组数据。
>
>ArrayList是应用更加广泛的动态数组实现，他本身不是线程安全的，所以性能要好很多。与Vector近似，ArrayList也是可以根据需要调整容量，不过两者的调整逻辑有所区别，Vector在扩容时会提高一倍，而ArrayList则是增加50%。
>
>LinkedList顾名思义是Java提供的双向链表，所以它不需要像上面两种那样调整容量，它也不是线程安全的。

3. 对比 Vector、ArrayList、LinkedList 有什么不同？
>Hashtable、HashMap、TreeMap都是最常见的一些Map实现，是以键值对的形式存储和操作数据的容器类型。
>
>Hashtable是早期Java类库提供的一个哈希表实现，本身是同步的，不支持null键和值，由于同步导致的性能开销，所以已经很少被推荐使用。
>
>HashMap是应用更加广泛的哈希表实现，行为上大致与Hashtable一致，主要区别在于HashMap不是同步的，支持null键和值等。通常情况下，HashMap进行put和get操作，可以达到常数时间复杂度的性能，所以它是绝大部分利用键值对存取场景的首选，比如，实现一个用户ID和用户信息对应的运行时存储结构。
>
>TreeMap则是基于红黑树的一种提供顺序访问的Map，和HashMap不同，它get、put、remove之类的操作都是O(log(n))时间复杂度，具体顺序可以由指定的Comparator来决定，或者根据键的自然顺序来判断。

4. [类加载过程](https://www.jianshu.com/p/dd39654231e0)？
>当代码逻辑使用涉及到某个类时(具体形式可以是new也可以是反射)，会通过类加载机制的流程加载这个类，流程：
>* 加载：默认由"双亲委派机制"(父类加载器委派)通过有能力加载的最高层次加载器加载类的class文件
>* 链接：将Java类的二进制代码合并到JVM的运行状态之中，具体包括：
>1）验证：确保加载的类信息符合JVM规范，没有安全方面的问题
>2）准备：正式为类变量(static变量)分配内存并设置类变量初始值的阶段，这些内存都将在方法区中进行分配。注意此时的设置初始值为默认值，具体赋值在初始化阶段完成。
>3）解析：虚拟机常量池内的符号引用替换为直接引用（地址引用）的过程。
>* 初始化：给静态内容赋予实际的初始值，顺序是先父后子，先完成父子的所有静态变量再构造方法
>___
>*能答出这些，可以认为你是对jvm类加载有一定了解的，如果面试人数多面试官比较赶时间的话可能不会再深究细节，但是也要做好准备，一些大公司的面试还是非常有可能会深挖下去的，能挖多深挖多深。*


## 【四、最后的总结】
回想起最初写此文的动机，最直接的动机是觉得弄懂了equals()与hashCode()之间的关系，觉得我可以表达得比网上的回答更清晰，才有写此文的想法。后来有些问题自己理解得并未深刻，也没有投入足够多的时间去搞明白，有点虎头蛇尾。但是不得不说这篇文章给了我很多前进的方向，为了整理好这些答案而去顺便学习巩固相应的知识，收获颇丰。

最后希望这篇文章对你能有所帮助，如有整理得不好的地方恳请指出，欢迎点赞，欢迎交流。

___

*学习知识 = 进食 + 咀嚼 + 消化 + 吸收
进食 = 阅读/学习，掌握基本理论、掌握赏析能力
咀嚼 = 做笔记整理/解读优秀作品（顺便再次阅读/学习）
消化 = 反复思考+理解
吸收 = 在实际生活学习或项目中尝试使用该知识、感受该知识
[——《如何高效学习》](https://book.douban.com/subject/25783654/)*
