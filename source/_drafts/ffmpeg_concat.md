---
title: FFMPEG实现快速连接视频 批量处理（友人向）
tags: ["計算機","技術","ffmpeg"]
updated: 2020-09-03
date: 2020-09-03
categories: "計算機"
---

># TL;DR
使用ffmpeg+系统脚本实现大量视频的连接

<!--more-->

# 前言

友人公司业务需要处理大量视频拼接，天下苦Pr久矣，问有没啥办法

FFMPEG：
> 一个编解码器的综合工具（开源），实现诸多聚合功能如视频的转码、分割、连接、转封装、序列合并、序列拆分等。

BAT/SH：
> 系统脚本文件格式，配合调用ffmpeg实现自动化连接。

基本思路：使用ffmpeg的copy功能连接素材，使用脚本实现全自动化。

# 基本环境(Base on Windows10)

ffmpeg[下载地址](https://ffmpeg.zeranoe.com/builds/win64/static/ffmpeg-20200831-4a11a6f-win64-static.zip)、[中文手册](https://www.quarkbook.com/wp-content/uploads/2019/10/ffmpeg%E7%BF%BB%E8%AF%91%E6%96%87%E6%A1%A3.pdf)。

连接的命令结构：
> ffmpeg -i "concat:input1.mpg|input2.mpg|input3.mpg" -c copy output.mpg

释义为：
- ``ffmpeg``：软件的位置
- ``-i``：表示输入，后接输入内容
- ``"concat:input1.mpg|input2.mpg|input3.mpg"``：表示连接，连接内容为``input1.mpg``、``input2.mpg``、``input3.mpg``
- ``-c``：表示连接方式，后接输入方式
- ``copy``：表示仅复制，不重新编码
- ``output.mpg``：输出的文件


ffmpeg解压出来后，尝试调用：
1. Win + R 调出运行界面，输入``CMD``调用command
2. ![](/asset/images/技术/ffmpeg_concat/01.png)如果正常，会出现下面一堆乱七八糟的命令。
3. 调用命令：切换到待处理的工作目录：我此次是在“D:\week5\output\finalvideo”，则``cd D:\week5\output\finalvideo``![](/asset/images/技术/ffmpeg_concat/02.png)