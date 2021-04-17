---
title: FFmpeg+AnotherGUI實現Windows上進行ProRes 422編碼
tags: ["計算機","影視","FFMpeg"]
updated: 2018-05-21
date: 2018-05-21
categories: "影視"
---

## 方法來源

[How to Export Apple Pro Res on a PC Using Windows](https://www.youtube.com/watch?v=HcBHItw4niM)

## 材料

- [FFmpeg](https://ffmpeg.zeranoe.com/builds/)（[github地址](https://github.com/FFmpeg)）。官方提供了靜態版（Static，無動態鏈接庫）、共享庫版（Shared）、構建版（Dev，一堆頭文件）。此處下載Static或Shared版本

- [AnotherGUI](http://www.stuudio.ee/anothergui/)是一個編碼器前端（高效並行處理），支持大量轉碼工作管理和調度。

- 一個基於H.264編碼的視頻，格式MOV、MP4等皆可

## 基本原理

把已經渲染好的基於H.264編碼的視頻，通過FFmpeg進行轉碼。 AnotherGUI是一個圖形界面操作者，協同管理和調度。
<!--more-->
## 過程

- FFmpeg解壓，執行文件``ffmpeg.exe``在``/bin``中
![](/asset/images/技术/prores/01.png)

- AnotherGUI安裝也是一把梭，畫面簡潔明了，常用英語
![](/asset/images/技术/prores/02.png)

- AnotherGUI有指定FFmpeg，會在Path下尋找（但官方沒找到Setup for Windows，會找不到），可以直接在Executables裡重定向：
![](/asset/images/技术/prores/03.png)
（注：第一次打開默認Path都是空白的，上圖為過程演示）

- 轉碼模式選擇
![](/asset/images/技术/prores/04.png)

- 添加源文件（可直接拖拽），並在右邊的輸出文件夾選擇
![](/asset/images/技术/prores/06.png)

- Go
![](/asset/images/技术/prores/07.png)

- 輸出文件
![](/asset/images/技术/prores/08.png)

直接用QQ影音（自我反省）打開聽到一大堆撕裂聲音，直接用QuickTime打開
![](/asset/images/技术/prores/05.png)

## 結尾

貌似沒有找到直接進行ProRes Encode in PC的方法…？ （這就是FCP存在的理由嗎？）
