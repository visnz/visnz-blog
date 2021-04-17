---
title: flv/mkv文件提取pr可導入格式
tags: ["影視"]
updated: 2019-10-17
date: 2018-08-09
categories: "影視"
---

### FLV
早期視頻導入flash後導出swf體積龐大，flv（Flash Video）格式早期產生用於解決這個問題。 flv是**flash文件作為外殼保護（封裝）視頻**，並轉換成串流格式。

同時：

1. 外殼可以保護原視頻內容、版權等

2. 串流媒體傳輸支持在網絡上進行點播（視頻點播網站常用，現在逐漸被H5取代）

3. 視頻多用h.264編碼，音頻多用acc或mp3，但是有一層外殼，可以直接提取

4. pr並不是沒辦法導入flv，只要有相應編解碼器就可以導入（早期pr能解H.263，可以導入早期flv視頻）pr用的編解碼器體系參見AME，導入不了大多是flv的封裝格式AME非能解

解決辦法：

1. 直接對flv文件進行去外殼+重新封裝（**小丸工具箱-封裝，flv進去mp4出來最暴力**）

2. 抽出視頻（含外殼）+抽出音頻，再手動封裝
<!--more-->

![小丸工具箱](/asset/images/技术/flv/02.png)

（支持批量）

![對比圖](/asset/images/技术/flv/01.png)
### MKV

mkv（Matroska格式的一種）提供容器格式，用於存放多條視頻、多條音頻、多份字幕等，同時也支持串流媒體傳輸，支持選單（像DVD一樣）

不能拉入pr的原因是包含多個黏在一起的視頻、音頻、字幕等，而無法作為一個單獨的素材導入，故需要提取

小丸工具箱自帶抽取工具（以及第三方抽取工具）
![小丸工具箱](/asset/images/技术/flv/03.png)

同時在封裝版面也提供了mkv封裝

### 碩鼠flv下載器

碩鼠也提供了bilibili專門的下載器（能突破限速，這個還是蠻實用的）

同時可以安裝上“碩鼠轉換”，可以直接轉換flv到mp4（暫無mov？），不過沒有參數可調，而且壓縮得很慘

![碩鼠](/asset/images/技术/flv/05.png)

(最後89M被壓剩14M)


另外在bilibili大視頻會分片，以及番劇沒辦法在“kanbilibli”直接找到（可以去kanbilibili上搜索，依然可以找到），碩鼠可以直接根據番劇地址下載

![碩鼠](/asset/images/技术/flv/06.png)
同時提供了“碩鼠合併”，可以直接只能拼合（不會刪除原分片）

### 更新

[bilibili嗶哩嗶哩下載助手](https://chrome.google.com/webstore/detail/bilibili%E5%93%94%E5%93%A9%E5%93%94%E5%93%A9%E4%B8%8B%E8%BD%BD%E5%8A%A9%E6%89%8B/bfcbfobhcjbkilcbehlnlchiinokiijp)