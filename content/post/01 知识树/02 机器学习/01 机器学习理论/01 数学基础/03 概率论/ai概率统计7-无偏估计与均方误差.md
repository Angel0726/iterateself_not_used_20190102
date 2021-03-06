---
title: ai概率统计7-无偏估计与均方误差
toc: true
date: 2018-07-27 13:39:28
---

# ai概率统计7-无偏估计与均方误差


# 缘由：


对无偏估计和均方误差的东西再进行探讨。


# 无偏估计




## 无偏性：


利用已知样本 \(X_1,X_2,\cdots \X_n\)能够得到参数的一个估计 \(\hat{\theta}\)，因此， \(\hat{\theta}\)可以写成 \(\hat{\theta}(X_1,X_2,\cdots \X_n)\)，对于不同的样本， \(\hat{\theta}\) 的值一般不同。因此，可以看成是关于样本的随机变量。因此它是可以求均值的：\(E(\hat{\theta})\)

如果\(E(\hat{\theta})\)等于总体的实际分布\(\theta\)，就说这个估计是无偏估计\(E(\hat{\theta})=\theta\)。

用 \(\hat{\theta}\) 去估计\(\theta\)，有时偏高，有时偏低，但平均来说，它等于未知参数\(\theta\) 。


## 举例子：




![mark](http://images.iterate.site/blog/image/180727/cmBJ4hFJhj.png?imageslim)




## 样本均值和方差是总体的无偏估计




![mark](http://images.iterate.site/blog/image/180727/l7134KcB72.png?imageslim)

为什么呢？我们先看下均值：

均值的无偏性


![mark](http://images.iterate.site/blog/image/180727/g5K2A59L2l.png?imageslim)

那么方差又是什么原因呢？

方差的无偏性

![mark](http://images.iterate.site/blog/image/180727/3IfHGd4f88.png?imageslim)
**上面这个没明白怎么推出来的？要自己推一下。**

标准差是有偏的。



下面在聚类里面或多或少会用到这个准则。


# 均方误差准则：


![mark](http://images.iterate.site/blog/image/180727/HjF1mclLD2.png?imageslim)

如果是无偏估计，所谓的均方误差就是估计量的方差




# COMMENT：


**再看下 感觉掌握的不全面**

**没有很明白**


## 相关资料：






  1. 七月在线 机器学习
