---
title: 位图提取路径，逆向logo，导入ae
tags: ["影視"]
updated: 2019-12-04
date: 2019-12-04
categories: "影視"
---

# 结果

从一张简单的位图里提取选区反求矢量路径
<!--more-->
# 原理

基础图像 -> 即可能保持结构地插值放大（多次插值等） -> 选区（手动增对比、平滑处理等） -> 建立工作路径并储存 -> 复制粘贴到ae

![](/asset/images/技术/pathtoae/origin.jpg)
![](/asset/images/技术/pathtoae/p6.png)
# 操作

![](/asset/images/技术/pathtoae/origin.jpg)

进行插值放大，可以根据需要多次插值（每次放大20%，逐次放大）

![](/asset/images/技术/pathtoae/p1.png)

选择黑色部分，平滑选区

![](/asset/images/技术/pathtoae/p2.png)

![](/asset/images/技术/pathtoae/p3.png)

使用路径选择工具选择右边的路径，存储路径

![](/asset/images/技术/pathtoae/p4.png)

![](/asset/images/技术/pathtoae/p5.png)

复制粘贴进ae即可

![](/asset/images/技术/pathtoae/p6.png)

或者使用 导出-> 导出路径到Illustrator ，在ai中保存为Illustrator 8可以导入到C4D，导入ae通过合成图层“create shapes from vector layer”

# 后文

1. [将位图转矢量图用什么软件效果最好？](https://www.zhihu.com/question/264000935) 如[inkscape](https://inkscape.org/)(软件)、[Vector Magic](https://vectormagic.com/)(在线、收费，效果有保障)、还有许多免费的但是效果各异（Autotracer等）
2. 这样的逆向只能根据表层，如果是贯穿的图形块还是得自己处理


# 参考

[https://www.jianshu.com/p/456157dfe0b0](位图快速转矢量图的5种方法丨工具篇)
