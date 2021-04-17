---
title: AE脚本大整合——桶子工具箱（自家用）
tags: ["Ae","影視","計算機"]
updated: 2020-06-28
date: 2020-06-28
categories: "影視"
---

## 前言

![界面图](https://v.guediao.top/mygithub/AeGlobalController/panel.png)

有一些js的开发经验，在ae上进行开发脚本帮助自己提升效率。
最早[使用脚本来完成批量操作](https://v.guediao.top/post/%E5%BD%B1%E8%A7%86/aescript/index.html)（最基本功能）
后来在抽取模板时，因表达式引用问题而萌生[全局属性控制器](https://v.guediao.top/post/%E5%BD%B1%E8%A7%86/aegc/index.html)想法。尽管后来印证并不是必要的。

到如今撰写第一个**大型脚本集成工具箱**，对AE运行时环境、逻辑排布等都有更进一步的了解（虽然也没什么用）。

总体来说，主要是解决目前自己的几个需求
1. 对于重装系统后搬迁、安装脚本的避免，集成各种常用脚本一个顶N。包括大杀器：脚本管理器
2. 中英文查找，对于刚切换到英文系统，字典是必要的
3. 表达式片段存储，再也不用每次都打开笔记本看一下啦。
4. 色板，这个是我非常需要的…………
5. 最后是网络连接功能，这个是未来的想法：**云素材库**、**云校本库**。
6. 也能算是给简历添上没用的一小笔
<!--more-->

## 结构简述

1. 脚本管理器：集成自常见脚本管理器，需要自选script文件夹，右边可刷新

![](https://v.guediao.top/mygithub/AeGlobalController/panel3.png)

2. 集成脚本

![集成脚本图](https://v.guediao.top/mygithub/AeGlobalController/panel2.png)

这里基本集成了业界流传的一些实用脚本（目前仅集成我个人用得较多的）。
这里所谓**集成**，是指**这一系列脚本已经内嵌在这个大的脚本之内**了

3. keyfast：是一个快速创建关键帧的脚本
    1. Fi = Fade in 创建透明度从0到当前目标值（默认100）的关键帧，Fo = Fade out
    2. Su = Scale up 创建缩放从0到当前目标值（默认100）的关键帧，Sd = Scale down
    3. Rl = Rotate left 旋转，Rr = Rotate right
    4. Cl = Clone，克隆已选中的关键帧
    5. Rv = Time Reverse，已选中的关键帧在时间上反转

4. motion2：可以参考[这里](https://www.zcool.com.cn/article/ZNDIwMzg4.html)，基本是原生功能
    1. Nul = Null 创建空物体作为已选图层的父级，可以作为控制器
    2. Buc = Bouce 弹跳表达式
    3. Bld = Blend 缓和表达式
    4. Bst = Brust 爆发效果
    5. Rop = Rope 连线效果
    6. Wap = Wrap 拖尾效果
    7. Str = Stare 注视关系
    8. Vig = 创建暗角

5. Ease 缓动功能（此部分也是拆分自motion2）：第一行是in参数，0~100，第二行是两者同时选，第三行是out。
6. AnchorMove 锚点移动（函数来自motion2，但是它本来只提供9宫格，我就改成了浮点函数，现在可以随意移动）。reset可以重新居中
7. 常用表达式片段（个人）。**可以自己在jsx文件的头部新增自己的表达式，定义功能**。

![](https://v.guediao.top/mygithub/AeGlobalController/panel4.png)


8. 色板：暂时没有拾色器，色板可长期存储，不过只有15个位，点击 push 可以推入新的颜色（通过#HEX）

9. 中英查找：这个是个人因为从中切换到英文版，一些效果器不知道英文叫什么，每次都要查很麻烦。（最大正向匹配法）

![](https://v.guediao.top/mygithub/AeGlobalController/panel5.png)

查找到后，可以在右边选择，按apply直接添加到已选图层

10. 调试器：提供log面板，同时也可以直接调用。调试器会直接调用``try{eval( $YOUR_INPUT$ )}catch(e){alert(e)}``函数

![](https://v.guediao.top/mygithub/AeGlobalController/panel6.png)

11. 本地调用：可以选择已经写好的内容直接调用os函数

![](https://v.guediao.top/mygithub/AeGlobalController/panel7.png)

从上到下内容依次是：记事本、计算器、画板，最后一个是**AE多开**

12. 测试版内容

包含了一个可以访问web的接口，可以输入http网址进行访问获取。filter可以进行内容筛选。

## 工程结构简述

1. 主框架=数据（脚本内置、设置保存的数据）+UI框架+注册函数（注册UI事件）+功能函数（执行各种功能）
2. 数据里包含：表达式、集成脚本的片段组，一个中英对照字典
3. 功能函数包含：表达式、集成脚本的片段函数，一大堆jsxbin代码的eval执行函数。另外是一些辅助函数log、web访问等

## TODOS
- [ ] 把ae的版本号抽象出来，使得修改比较容易
- [ ] 抽象出更多一些数据，不用上下来回翻。

## 后记

这次一共花费了五天，大概30小时左右。因为有一些基础，所以大部分是做整合和debug的工作。
拆分别的脚本、粘贴试运行。整合的话如对结构进行合理梳理等。还有一部分时间花在需求的整理上。由于曾经的程序员思想容易迷失作为PM的目标。

比较好的是通过这次训练找回了状态。

可能接下来一段时间都不会想碰ae脚本了。