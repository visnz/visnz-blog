---
title: 修正達芬奇xml剪輯表素材出入點錯誤
tags: ["影視","達芬奇","計算機"]
updated: 2018-09-03
date: 2018-09-03
categories: "影視"
---

![](/asset/images/技术/dvcxmlfix/logo.png)


## 背景
因為一些原因 需要將一段素材進行場景變換偵測（根據鏡頭切換，切割視頻），然後轉換成剪輯表跟素材，進行下一步的操作。在輸出剪輯表的時候，發生了“剪切時間點正確，但素材出入點錯誤”的尷尬局面。

## 場景偵測

達芬奇提供**場景偵測自動分切**的功能：

![](/asset/images/技术/dvcxmlfix/03.png)
![](/asset/images/技术/dvcxmlfix/04.png)

圖片一目了然，根據畫面變化率進行分辨對視頻進行逆向分析（所以一些漸變效果需要自己手動調整右邊的時間切段）

下面的紫色的線條可以上下拖動調整變化率敏感度

![](/asset/images/技术/dvcxmlfix/05.png)

將分切好的素材全選生成一個對應序列，在剪輯板塊直接導出XML文件（因為需要跟pr接駁，直接用了標準XML）
<!--more-->
## 問題
通常來說輸出的剪輯表應該是這樣的：

AB,C,DEF,GH,I

結果在PR中讀取是這樣的：

AB,A,ABC,AB,A

即：剪輯點是對的，但素材的起始點不對，全部回到素材的起始點了

![](/asset/images/技术/dvcxmlfix/06.png)

## 分析

1. 直接一個一個改治標不治本

2. 直接用達芬奇渲染分段素材，又擔心二次渲染對素材造成影響，以及無緣無故浪費機器性能

3. 直接拆剪輯表，把素材的出入點進行修改

## 實操

剪輯表的格式是普通的xml格式，用一些在線閱讀器可以更明朗地觀看：

![](/asset/images/技术/dvcxmlfix/02.png)

而其中出現問題的就在每一個素材剪輯段的標籤內：

![](/asset/images/技术/dvcxmlfix/01.png)

要做的就是**篩選出指定標籤裡的剪輯點同步到素材出入點上**

nodejs代碼：
```javascript
var fs = require("fs");
var xml2js = require('xml2js');
var parser = new xml2js.Parser();//用於解析xml為json對象
var builder = new xml2js.Builder();
fs.readFile(process.argv.slice(2)[0], "utf-8", function(err,data){
    if (err) {console.log("讀取文件失敗"); throw err;}
    parser.parseString(data, function(err,res){
        if(err) throw err;
        var medialist=res.xmeml.sequence[0].media[0]//獲取media列表
        var vlist=medialist.video[0].track[0].clipitem
        var alist=medialist.audio[0].track[0].clipitem
        for(clip of vlist){
          clip.in[0]=clip.start[0]
          clip.out[0]=clip.end[0]
        }
        for(clip of alist){
          clip.in[0]=clip.start[0]
          clip.out[0]=clip.end[0]
        }
        var outxml = builder.buildObject(res);
        fs.writeFile("output01.xml", outxml.toString(), err1 =>{
            if (err1) {throw err1;}
            console.log("成功寫入文件");
        })
    })
})
```

感謝大佬的代碼。 [引用來源](https://www.jianshu.com/p/a7a2b693d003)