---
title: 算法 数独Sudoku
toc: true
date: 2018-07-27 17:22:58
---


数独问题：

解数独问题，初始化时的空位用‘.’表示。
 每行、每列、每个九宫内，都是1-9这9个数字。


![mark](http://images.iterate.site/blog/image/180727/a4imgAGeFE.png?imageslim)



数独Sudoku分析
 若当前位置是空格，则尝试从1到9的所有
数；如果对于1到9的某些数字，当前是合法
的，则继续尝试下一个位置——调用自身即
可。


![mark](http://images.iterate.site/blog/image/180727/4b0g2d0aIL.png?imageslim)

代码如下：


![mark](http://images.iterate.site/blog/image/180727/7H40d32i4A.png?imageslim)

非递归数独Sudoku


![mark](http://images.iterate.site/blog/image/180727/59ELEa1JiC.png?imageslim)

COMMENT：

REF：




  1. 七月在线 算法

