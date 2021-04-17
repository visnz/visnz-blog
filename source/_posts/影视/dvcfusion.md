---
title: DaVinci/Fusion 节点式效果软件初体验:Tracker跟踪效果
tags: ["影視","達芬奇","計算機"]
updated: 2018-06-03
date: 2018-06-03
categories: "影視"
---

## 背景

（Adobe用户习惯剥离计划进行中）

因为最新的Davinci15把BlackMagic自家的Fusion内置了，现在基本集素材整理、剪辑、特效、调色、调音和渲染于一身，效果在达芬奇里面做也是方便点的。借这个机会尝试一下节点式效果工具

![结果图](/asset/images/技术/fusion/01.png)
达芬奇15中的Fusion页面

视频效果:
<video src="/asset/images/技术/fusion/效果.mov" controls="controls">
您的浏览器不支持 video 标签。
</video>

<!--more-->

## 素材与需求

（其实是过段时间bdf制作希望高点逼格）素材是多人出入场的舞蹈，将人物的名字附加到舞蹈者的运动趋势上

于是随机找了一段电脑里**带有运动趋势的素材**和**一个白条**做尝试
<video src="/asset/images/技术/fusion/原片.mov" controls="controls">
您的浏览器不支持 video 标签。
</video>

图片素材
![素材](/asset/images/技术/fusion/02.png)

临摹的想法来源：
[BDF2018宣传片 after 1:20](https://www.bilibili.com/video/av22787517)

## 操作

导入两部分素材，在时间线上部署底层素材
![](/asset/images/技术/fusion/03.png)

直接切换到fusion工作台
![](/asset/images/技术/fusion/04.png)

节点式主要是以清晰明朗的效果器结构与关系来展示复杂的效果逻辑，这一点比ae在层级控制上有更多的灵活性
![](/asset/images/技术/fusion/05.png)
图中为节点面板，左边是媒体素材，右边是媒体的输出，要做的就是在这两个节点之间添加效果器

为输入素材添加跟踪器，并添加节点进行跟踪，跟踪……素材里的女孩的蝴蝶结
![](/asset/images/技术/fusion/06.png)
![](/asset/images/技术/fusion/07.png)
下面是添加中间节点的效果器 中间是跟踪结果 右上角向右跟踪

添加人名条并将其运动轨迹指定为跟踪器的分析结果
![](/asset/images/技术/fusion/08.png)
左下角将新素材连接到跟踪器 右边切换到跟踪模式，切换到匹配移动(match move)模式，则结果会出现人名条已经被附加到跟踪器的轨迹上

修改人名条的相对位置匹配到指定点上
![](/asset/images/技术/fusion/09.png)

简单的节点效果制作就完成了，切换回剪辑模式即可继续剪辑。因为效果是基于素材的，在剪辑里没有额外增加新的素材，整个工程更加简洁明了（pr和ae你们自己反思反思）
![](/asset/images/技术/fusion/10.png)

## 结尾

- 提供了更灵活的调节工具（当然需要你的硬件）

- 提供了更清晰明朗的工程结构

- **最最重要的是，它可以在交付里重新生成片段xml，自定义帧余量渲染套底，整个回批的素材包只包括必须素材的必须片段，会小很多很多！**

![](/asset/images/技术/fusion/11.png)
前排抱走~~诸君的~~老婆
