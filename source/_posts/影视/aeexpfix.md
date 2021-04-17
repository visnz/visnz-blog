---
title: 修復ae中英版本差異導致js表達式錯誤
tags: ["Ae","影視","計算機"]
updated: 2020-03-14
date: 2018-11-02
categories: "影視"
---

![](/asset/images/技术/aeexpfix/ae.png)

# 背景

下載一些模板打開之後發現預覽窗口下警告“表達式錯誤”，導致效果無法顯示

原因：通常是因為原來的模板，在使用系統組件的表達式中引用了英文，在中文的ae中打開後，系統組件無法被正確引用。

# 解決思路

## 1. 手動修bug法：在圖層表達式中修復引用

把``英文名引用``換用``中文名``，**量小的時候建議修復**，量多的話參考第二個解決思路
<!--more-->
中英的關係如下：

1. 滑塊 = Slider

2. 角度 = Angle

3. 複選框 = Checkbox

4. 顏色 = Color

5. 點 = Point

6. 圖層 = Layer

7. 3D 點 = 3DPoint

![](/asset/images/技术/aeexpfix/01.png)

通過提示直接查找每一個錯誤的引用，將引用（在圖層裡，通常是紅色代表出錯）的表達式裡的英文，轉成對應的中文

![](/asset/images/技术/aeexpfix/02.png)

發現錯誤，找到表達式如下：

![](/asset/images/技术/aeexpfix/03.png)

打開“Your Text”圖層，效果如下

![](/asset/images/技术/aeexpfix/04.png)

將“Fast Blur”改為“快速模糊（舊版）” 提示仍有錯誤，根據提示將“Blurriness”改為“模糊度”，成功改正錯誤

### 2020.3.14 追加修订
> 可以将最后一个括号内的内容，直接改成“1”。
> 如：xxx.effects("cont")("3D 點")
> 改成：xxx.effects("cont")(1)

## 2. 一勞永逸法：修改底層中英引用

軟件裡的系統組件的語言文本，將中文引用改為英文引用，其他不變，使其適配英文表達式。 **出現大量錯誤時候推薦，一勞永逸**

在Support Files-zdictionaries（win）或Contents/Dictionaries/zh_CN（mac）文件夾（語言文件相關）下，找到after_effects_zh-Hans.dat

改動常見的語言錯誤如下圖。 （中英對應解決方案1中的中英映射）

![](/asset/images/技术/aeexpfix/05.jpg)

之後 reload AE 即可

# 總結

你看這個ae英文版它又大又圓，真香。

# 參考資料

- [貼吧吧友解決方案](http://tieba.baidu.com/f?kz=5626448845&red_tag=m3200829573)

- [表達式修復工具](http://www.lookae.com/universalizer3/)

- [詳細修復及原理博客](https://blog.part3.me/ae-fix-expression-error/)