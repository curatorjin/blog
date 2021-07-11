---
layout: post
title: "重新思考面向对象"
date: 2021-07-02 03:08:10 +0800
tags:  编程思维
---

# 重新思考面向对象

> 封装 继承 多态这些只是面向对象的特征，并非其本质

## 经典例子
> Jeff Goodell：请你用尽量简练的语言解释一下，究竟什么是面向对象的软件？

如果我是一个“洗衣”对象，你可以把脏衣服给我，然后告诉我说：“请帮我把这些衣服洗了吧！”而我恰好知道旧金山最好的洗衣房在哪，并且我会说英语，兜里也有美元。于是我出门大了一辆出租车，告诉司机带我去位于旧金山的洗衣房。我到了那里洗好衣服之后，又坐车回到这里。我把洗好的衣服交还给你，说：“你的衣服已经洗好了。”

你并不知道我是怎么做到的。你不知道哪里有洗衣店，也可能只会说法语，或者是兜里没钱，连车都打不了。但是我知道怎么完成这项人物，而你不需要指导任何细节。所有的这些复杂流程都隐藏在我的内部，而我们之间可以高度抽象地互动。

## 面向对象与面向过程并不冲突
> “即使是被称为面向过程的C语言，也完全可以写出面向对象的代码”

谈到面向对象，总有人会将其与面向过程作比较，并认为之间具有差异。在我看来二者之间并不冲突。

以[经典例子](#经典例子)来说，总体来看，洗衣服的过程是面向对象的，你让我去洗衣服，并得到了洗好的衣服作为结果。但对于具体的操作而言，“我”的洗衣服的过程却是面向过程的：

1. 打车去洗衣房
2. 在洗衣房洗好衣服
3. 坐车回到这里

在这里的第二步，“我在洗衣房洗衣服”又可以看作是一个面向对象的交互过程：我并不需要知道衣服应该怎么洗，只需要把钱和脏衣服交给洗衣房执行就可以了。
同样的，对于总体的洗衣操作来看也可以看作是面向过程的操作，只不过这个过程只有“你把脏衣服交给我”一个步骤。

面向对象与面向过程并不冲突，他们表达的只是两种看待问题的方式。

## 面向对象是一种编程思想

> “我们应该采取行动，认识到面向对象编程的危险，并努力学习函数式编程。”

很多文章不知道是出于何种目的，会给面向对象扣一个“糟透了”的帽子。然而其文中提到的“面向对象”的“缺点”却更多的着重于形式。我们都知道面向对象的四大特征是“抽象”、“封装”、“多态”和“继承”。那么，满足了这四个特征的就一定是面向对象了吗？ 如果真的按照这种方法去归类，难免会出现“按图索骥”的错误。这四大特征只是特征，而并非本质。

面向对象是一种思想，代表的是一种看待问题的方式。还是以[经典例子](#经典例子)来看，用哪一种思路来看待问题取决于是**我要去洗衣服**还是**我找人去洗衣服**。从这个角度上来说面向对象也好面向过程也好，并没有优劣之分，只有涉及到具体问题的应用时，才有合适与否之别。

当你的思路确定下来了，在完成整体事件的描述或分析之前，都不应该让其他的思想介入你的分析过程。在我看来，使得面向对象臭名昭著的原因无非是因为你用着面向对象的语言(或框架)，却使用了面向过程的思想。就好像在把脏衣服交给了别人，却没有把钱或者车钥匙给他。这种思维混乱所造成的不良后果，怎么能让一开始所选择的思维方法背锅？

因此，面向对象并不是简单的封装、继承。我们在学习了面向对象语言的这些特性之后，仅仅只是了解了**这里可以这么用**的问题，而**这里为什么这么用**的问题，值得我们一直去思考。

## 总结：关于方法与目的
> 学而不思则罔，思而不学则殆

对于方法何时使用、如何使用的问题，本人目前也只是略有所悟，有时间会结合相关代码再作具体问题的表述。本篇只是对于面向对象的概念重新作出思考，希望能有所启发。

这里预告一下后续会讨论到的一些问题，也算是开个坑：
1. 粒度与可用性的权衡
2. 依赖对于模块化的干扰
3. 关于资源的共用

最后说一句，方法、框架、思想只是工具，而真正的核心在于你想做什么。舍弃了核心目的，盲目地追求技术是不可取的。


### 参考资料
- [面向对象已死，OOP永存](https://www.gamedev.net/blogs/entry/2265481-oop-is-dead-long-live-oop/)
- [面向对象就是一个错误](https://blog.csdn.net/weixin_42232219/article/details/113764592)
- [什么是面向对象编程思想](https://www.zhihu.com/question/31021366)

### 引申链接
> 使用面向对象时的一些规范

- [SOILD编程规范](https://www.jianshu.com/p/1c6498da3862)
- [数据库规范化理论](https://zhuanlan.zhihu.com/p/344351869)