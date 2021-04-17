---
title: 貓國建設者 長篇自動化腳本
tags: ["遊戲","技術","腳本","Web","計算機"]
updated: 2019-08-16
date: 2019-08-13
categories: "計算機"
---

已经实现的效果：

![](/asset/images/技术/moe/icon2.png)


## 前言

沉迷貓國建設者卻不經常上，放到了PC上挂機。放到了PC還是沒辦法做到三分鐘看一次處理一次，索性用js寫個腳本。

到後半部分，單純寫單個腳本已經不夠完成業務邏輯，把接口抽象出來，進行腳本的體系化構建：接口、常量、邏輯等

## 思路

通過瀏覽器的開發工具，定位頁面按鈕，設置定時回調完成腳本動作
<!--more-->
## 過程簡述

1. 存檔導出粘貼進來即可，在頁面右鍵調出調試工具（DevTool）進入控制台
    ![](/asset/images/技术/moe/01.png)
2. <tag>此步驟可能引入漏洞產生風險</tag>。控制台下方輸入``allow pasting``開啟腳本粘貼。
3. 使用CSS選擇器獲取元素：需要點擊或獲取信息的部件，通過查看元素獲取，剪貼板會獲得一個字符串，如：``div.res-row:nth-child(6) > div:nth -child(6) > div:nth-child(1)``
    ![](/asset/images/技术/moe/02.png)
    ![](/asset/images/技术/moe/03.png)
4. 函數調用：
     - 使用``$("#ELEMENT_ID").text()``獲取內容，返回字符串，可以用於判斷
     - 使用``$("#ELEMENT_ID").click()``模擬點擊
     - 更多功能參考[jquery手冊](https://www.w3school.com.cn/jquery/jquery_reference.asp)
5. 使用``async``回調來設置異步事件(原理層面的解釋)：
    ```js
    // 設置一個0延遲的異步回調，相當於一個新的並行線程
    setTimeout(async()=>{
        while(true){
            // 設置一個輪詢的回調事件：阻塞一段時間執行某一部分內容
            await new Promise(resolve=>setTimeout(resolve,MS))
            // TODO
        }
    },0)
    ```

## Example

空餘全派遣為獵人，設置定間隔點擊``派出獵人(N次)``按鈕

```js
// 設置一個0延遲的異步回調，相當於一個新的並行線程
setTimeout(async()=>{
    while(true){
        await new Promise(resolve=>setTimeout(resolve,100000))
        // 100秒點擊一次獵人
        $("#fastHuntContainerCount").click()
    }
},0)
```

![](/asset/images/技术/moe/04.png)

或者換用更簡便的``setInterval(callback,ms)``,上文可以改寫為:

```js
// 設置一個0延遲的異步回調，相當於一個新的並行線程
setInterval(()=>{$("#fastHuntContainerCount").click()},100000)
```

在控制台裡粘貼執行即可

## 腳本體系化

### 常量層
這一層記錄從遊戲頁面抓取的信息與腳本的常量信息，包含部分按鈕位置信息、腳本默認間隔時間等。

        const defaultDelay = 60000
        const Jobs = {"伐木工": 0,"農民": 1,"學者": 2,"獵人": 3,"礦工": 4,"牧師": 5,"地質學家": 6,"工程師": 7}

### 接口層

把遊戲操作經過常量層的信息，抽像出可以調用的接口，比如定位到資源換算按鈕、職業分配加減的按鈕等操作。

### 腳本邏輯層

把接口組合成腳本邏輯，如簡單的換算所有木材、分配職業、自動調整最低農民<tag>TBD</tag>、保存遊戲、獲取當前木材數量、換算腳手架、進入某個面板，同時設定面板展示信息與執行間隔（使用``set/clearInterval()``函數），如管理工作方法、定義面板：

        管理Jobs = () => {
            _記錄當前面板Index()
            _進入管理面板()
            _管理Jobs()
            _返回記錄面板Index()
        }
        AllOperators = [{
            panel: "基本",
            list: [
                { DisplayName: "抬頭看天空", timer: fastDelay },
                { DisplayName: "自動打獵" },
                { DisplayName: "讚美太陽" },
                { DisplayName: "管理Jobs", timer: verySlowDelay },
                { DisplayName: "小貓升職器", timer: verySlowDelay },
        ]}

### UI邏輯層

按照腳本邏輯提供的面闆對象進行渲染、註冊事件

具體可以直接查看[源碼](https://github.com/visnz/Allend-practice/blob/master/js/moejq.js)

可以直接在瀏覽器的``console``直接C/V/Enter[這部分內容](https://github.com/visnz/Allend-practice/blob/master/js/dist/_moejq.js)

### 雜記

1. 使用了``"use strict";``嚴格模式。
2. 建立了簡單的MVC模型，由M生成V並註冊C，只註冊了簡單事件通過C修改V（畢竟沒有強交互邏輯）
3. 左邊的合成面板跟職業面板是固定的，可以直接通過索引獲取。但是建築物不是固定的。
4. for循環連點採集貓薄荷的<tag>卡機刨~~木~~墳法</tag>，狂吃內存刷貓薄荷。中速（每秒10000次，可以出10K貓薄荷），定期保存。
5. UI層使用了多層map/reduce來形成統一渲染，註冊每一個事件都使用了``setInterval()``的回調
6. 寫了一個div專門作用於log，使用logThis()進行屏幕輸出。
7. 特殊的樣式直接寫死在編碼中，其餘使用了網頁原本的css樣式
8. compliers：寫了一個``.vscode/task.json``設置，用於優化js：

        "java -jar /usr/bin/closure-compiler-v20190729.jar --js ${file} --js_output_file ${fileDirname}/dist/_${fileBasename}"

## 後記

官方有提供機器人[小貓科學家](https://likexia.gitee.io/cat-zh/wiki/?file=004-%E7%AC%AC%E4%B8%89%E6%96%B9%E5%B7%A5%E5%85%B7/02-%E7%8C%AB%E5%92%AA%E7%A7%91%E5%AD%A6%E5%AE%B6)，喜歡自己動手可以自己寫一寫