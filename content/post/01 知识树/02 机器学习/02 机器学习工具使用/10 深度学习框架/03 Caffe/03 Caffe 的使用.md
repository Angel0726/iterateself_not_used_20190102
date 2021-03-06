---
title: 03 Caffe 的使用
toc: true
date: 2018-08-18 21:45:23
---

# 需要补充的

- 还是要找本书系统的学习一下，简单的了解在关键时候就只能疲于奔命查一些鸡毛蒜皮的东西。
- 这个只是简单的看了下，没有自己实际操作，自己尝试过之后进行修正和补充。
- 寒小阳的github上有对于caffe源码的解析。要自己走一遍。



# Caffe 的使用


对 Caffe 的使用进行总结：


# 这种训练方式不用写代码

1. Resize 图片 ， 转换存储格式(LMDB/LevelDB)
2. 定义网络结构（编辑prototxt ）比如说多少层，每层什么样的参数
3. 定义solver （编辑另一个prototxt ） 定义一些优化的方法
4. 一行命令开始训练（可以基于已有的权重赋值）

# 大体流程如下：


![mark](http://images.iterate.site/blog/image/180727/5hHjdB0ckJ.png?imageslim)

数据集图片会转存到数据库种，因为我们会频繁的读写这部分数据。它的backend是支持levelDB和LMDB的，然后在这个数据库种进行平凡的读写。**Lrn是什么？levelDB和LMDB是什么？非常想知道代码里面都是怎么实现数据库与计算之间的并行的。不同的thread之间是怎么交互的这里？**


## 第1步：转化格式

![mark](http://images.iterate.site/blog/image/180727/HjG5f77HLc.png?imageslim)

### 第2步：定义层次结构




![mark](http://images.iterate.site/blog/image/180727/BbDlaHEfIL.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/k2e0LDd4CJ.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/FDl4641c06.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/BCLfje9gFH.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/H5DgHJLfC8.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/l8eLhd7jK4.png?imageslim)






![mark](http://images.iterate.site/blog/image/180727/gBAbCibhgk.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/HI2j69I1D7.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/I16bBCF01k.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/0FLI74FGE1.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/8F2gfLLiJd.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/jlk7k6KD24.png?imageslim)




### 第3步：定义solver




![mark](http://images.iterate.site/blog/image/180727/J6JDC6lFKH.png?imageslim)

第4步：训练


![mark](http://images.iterate.site/blog/image/180727/mim1AjlfE0.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/d435D987im.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/GalmgDEcjc.png?imageslim)




## 模型库首选：model zoo


AlexNet 、VGG 、GoogLeNet 、ResNet


![mark](http://images.iterate.site/blog/image/180727/J2jAC5KLJd.png?imageslim)




## 关于fine-tuning




### 如果层次不变 ， 只需修改输入输出




![mark](http://images.iterate.site/blog/image/180727/2AhmD2lm4j.png?imageslim)


![mark](http://images.iterate.site/blog/image/180727/F1I1jkEGjG.png?imageslim)




### 如果层次改变 ， 添加 / 删减层次




![mark](http://images.iterate.site/blog/image/180727/fgcGLlD8e9.png?imageslim)




### fine-tuning技巧/注意点


优先学习权放在新加层：




  *  每一层都有控制学习率的参数: blobs_lr


  * 一般会把前面层学习率调低，最后新加层调高


  * 你甚至可以freeze前面的层次不动


  * 一般fine-tuning的前期loss下降非常快，中间有个瓶颈期，要有耐心


在solver处调整学习率：


  * 调低solver处的学习率（1/10， 1/100）


  * 记住存储一下中间结果，以免出现意外




## pycaffe




### Import caffe加载库






  * caffe.net是加载/运行/训练模型的主类(接口)


  *  caffe.Classifier和caffe.Detector是针对识别/检测的接口


  * caffe.SGDSolver最优化


  * caffe.io负责输入输出和预处理


  * caffe.draw可以画出网络结构图




### 加载所需库：






  * import numpy as np


  * import matplotlib.pyplot as plt


  * from PIL import Image


  * import caffe




### 选择GPU或者CPU






  * #使用cpu


    * caffe.set_mode_cpu()





  * #使用gpu


    * caffe.set_device(0)


    * caffe.set_mode_gpu()







### Pycaffe训练


定义网络结构


![mark](http://images.iterate.site/blog/image/180727/137gEie1cJ.png?imageslim)

载入solver


![mark](http://images.iterate.site/blog/image/180727/EGa9L7kahd.png?imageslim)



![mark](http://images.iterate.site/blog/image/180727/HLE4FB0HdK.png?imageslim)

Solver训练


![mark](http://images.iterate.site/blog/image/180727/2G31iC2dJJ.png?imageslim)




### Pycaffe用CNN抽取特征


做完前向运算取出某层输出


![mark](http://images.iterate.site/blog/image/180727/almkAh3I4J.png?imageslim)

更详细的流程可参考 https://github.com/HanXiaoyang/image_retrieval/blob/master/compute_fea_for_image_retrieval.py


### Pycaffe图像识别


![mark](http://images.iterate.site/blog/image/180727/ABB6d2B9fF.png?imageslim)




### Pycaffe画出你的网络结构


你在conv.prototxt中定义好了卷积层如下

![mark](http://images.iterate.site/blog/image/180727/F147C5dk3a.png?imageslim)

![mark](http://images.iterate.site/blog/image/180727/hhem5clh5l.png?imageslim)

python python/draw_net.py conv.prototxt my_net.png


![mark](http://images.iterate.site/blog/image/180727/cJAHfhHHgG.png?imageslim)





## 相关资料

- 七月在线 深度学习
