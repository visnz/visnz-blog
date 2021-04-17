---
title: ESTK上手，AE腳本撰寫，提升模板替換速率
tags: ["Ae","影視","計算機"]
updated: 2019-10-17
date: 2019-10-17
categories: "影視"
---

## 寫在前面

**ESTK是很強大的東西，別再抱怨Adobe軟件不夠靈活了**

[ESTK](https://www.adobe.com/devnet/scripting/estk.html)是*ExtendScript Toolkit Archives*，是Adobe官方的基於Adobe軟件運行時的腳本開發工具，即可以用於所有Adobe軟件操作的接口。

用途：編寫所有adobe插件、批量操作、圖形計算等等

### 實戰數據：

AE腳本撰寫，提升模板替換速率：100條模板渲染，大約一小時腳本撰寫

流程|基本條|每條|修改|預計時間|人工干預|效率提升
-|-|-|-|-|-|-
原模板||10min|1min|**1100min**|*每11min修改一次*|
分層|10min|1min|修改1min|**210min**|*每2min修改一次*|效率提升370%。
腳本自動|10min|1min|0|**170min**|*無需干預，需監督*|效率提升23%

if( 腳本撰寫時間 < 每條修改時間\*渲染數量+*懶癌程度* ) then 撰寫腳本

<!--more-->

## 背景

ae模板提供了基於統一設置好動畫，替換內容進行輸出的基本結構。

1. 最早的替換結構：在合成內部進行內容替換

在較新的版本裡提供了[``Essential Graphics``](https://helpx.adobe.com/cn/after-effects/using/creating-motion-graphics-templates.html)（中文翻譯是“基本圖形”）的功能，將一個合成暴露一定的

2. 使用基本圖形，其實就是把那些內部的內容（比如文本、位置）抽出來（被稱為主屬性），並封裝成一個新的數據結構(.mogrt)，可以直接在Pr中聯動使用。

基本圖形的好處是Ae跟Pr甚至更多軟件之前的修改操作會更有主動性。

但是使用這些是在結構上進行優化，要解決批量替換的問題，還是得靠腳本：

## 邏輯

單一替換內容（文本、圖片）的腳本邏輯基本如下：

1. 根據合成名稱找到合成
2. 替換指定圖層內容到新內容
3. 添加到渲染任務
4. 設置輸出模塊、輸出位置
5. 點擊渲染

在這個邏輯之上，我寫了一個很常規的模板**批量替換文本+自動渲染**的腳本：
（因為直到最新的16.1，ESTK依然沒有對``Essential Graphics``的修改支持，所以只能選定到必須修改的圖層）

```js
var renderFolderTag="節目條"    // 這個是文件名前綴
var targetComp="節目條render"   // 這個指定要渲染的合成
var motionComp="節目條文字部分"  // 這個指定要替換的合成
var motionCompLayerIndex=13     // 這個指定要替換合成的圖層
var outputModule1="TGA"         // 指定輸出預設名，渲染面板先保存成模板
var dir="G://Output"            // 指定輸出的位置
var Content=[                   // 要替換的內容
    "李雷",
    "韓梅梅"
]

// 這一部分用於從targetComp查找合成的編號，motionComp同
var index=1
while(true){
    try{
        if(app.project.item(index).name==targetComp){
            targetComp=index
            break;
        }
        index++    
        }catch(e){
            alert(e.toString())
        break;
    }
}
// 針對Content進行循環
for(var i=0;i<Content.length;i++){
    app.project.item(motionComp).layer(motionCompLayerIndex).property("sourceText").setValue(Content[i]) 
    // 替換目標圖層的文本
    app.project.renderQueue.showWindow(1)
    // 打開渲染面板
    app.project.renderQueue.items.add(app.project.item(targetComp))
    // 添加合成到渲染
    app.project.renderQueue.item(1).outputModule(1).applyTemplate(outputModule1)
    // 選擇輸出模板
    var new_data = {
        "Output File Info":{
            "Base Path":dir,
            "Subfolder Path":renderFolderTag+(i<9?"0"+(i+1):(i+1))+" "+Content[i],
            "File Name":Content[i]+(outputModule1=="TGA"?"_[#####]":""),
            // TGA等圖片序列需要後面加 [#####]
        }
    };
    // 指定輸出的參數
    app.project.renderQueue.item(1).outputModule(1).setSettings( new_data );
    // 應用輸出參數
    app.project.renderQueue.render()
    // 調用渲染
    app.project.renderQueue.item(1).remove()
    // 刪除渲染任務
}
```

## 寫在最後

模板替換是一個較為基礎、重複的，又是視頻製作不可缺失的一部分。可以用腳本來提升工作效率也是再好不過了。缺陷是ESTK目前大部分資料都還是**純英文**

## 參考資料

- [After Effects Scripting Guide](http://docs.aenhancers.com/)