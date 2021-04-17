---
title: 谷歌娘、网易云、B站、emipm等视音频提取经验分享（会更新的）
tags: ["Google","技巧","计算机","影視"]
updated: 2020-01-13
date: 2020-01-13
categories: "影視"
---

---
## 前言 

此文提供基于2020年1月13日可行的提取技巧（不负责版权问题），不负责官方反提取技术提升带来的技巧失效。（有空就更新）

目前仅记录因工作过程涉及提取素材的网站，后续将持续更新。目前搜集了包含：

谷歌娘（谷歌翻译、AI语音朗读）、网易云音乐抓取、emipm、B站

<!--more-->

## 谷歌娘（谷歌翻译）

[谷歌翻译](https://translate.google.cn/)中国区的服务还没有撤离。选择语言在左边输入内容，按F12开启控制台。

![](/asset/images/毕业后/voiceget/01.png)

按朗读，右边便会截取返回的media报文

![](/asset/images/毕业后/voiceget/02.png)

在新页面按 保存 或另存为就行。
```
https://translate.google.cn/translate_tts?ie=UTF-8&q=%E5%A5%87%E8%A7%82%E8%AF%AF%E5%9B%BD%E5%95%8A%E9%99%9B%E4%B8%8B&tl=zh-CN&tk=578409.942673&client=webapp
```
另：这个get报文带有一个token用于认证（目测是有时效性的），直接调用get可能不可取

## 谷歌娘（AI语音朗读）（科学上网）

谷歌提供了另外一个基于深度学习的[语音引擎](https://cloud.google.com/text-to-speech/)（用谷歌云可以有限免费跑），有试用版试用版。提供了比谷歌翻译**更好的语调控制、节奏控制**（中文还是一般般，企业宣传片方面还不够气势，但是基本朗读听起来比翻译的清晰。英文的挺不错）

目前没有什么有效的方法抓取，后来直接用**录屏**（比如[Ffmpeg](https://ffmpeg.zeranoe.com/builds/win64/shared/ffmpeg-4.2.1-win64-shared.zip)、Bandicam）

## 网易云音乐抓取

提取音乐网页链接

![](/asset/images/毕业后/voiceget/03.png)

![](/asset/images/毕业后/voiceget/04.png)

提取id 补充在这里：``http://music.163.com/song/media/outer/url?id=提取到的ID``

新网址在网页打开就行。有时效性认证，分享慎重。VIP的还无法下载。

[参考链接](https://blog.csdn.net/qq_42651904/article/details/87893739)（其中推荐的jojo试用过，可能我本地网络连接有问题，不置可否）

## emipm

方法跟[谷歌娘（谷歌翻译）](#谷歌娘（谷歌翻译）)很像，emipm点击播放音频直接在网页代码里更新了音频地址：

![](/asset/images/毕业后/voiceget/06.png)


## B站

B站视频提取直接用[bilibili哔哩哔哩下载助手](https://chrome.google.com/webstore/detail/bilibili%E5%93%94%E5%93%A9%E5%93%94%E5%93%A9%E4%B8%8B%E8%BD%BD%E5%8A%A9%E6%89%8B/bfcbfobhcjbkilcbehlnlchiinokiijp)（谷歌插件商店）

![](/asset/images/毕业后/voiceget/05.png)

## 总结
