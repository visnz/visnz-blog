---
title: Linux上调用ffmpeg组件压制字幕
tags: ["影視","FFMpeg","計算機"]
updated: 2018-12-28
date: 2018-12-28
categories: "影視"
---

## 背景
N久之前幫人拍字幕送去審查，這都9102年了才送回來反饋。

修改完要渲染了，用慣Linux不想回Windows，壓字幕又要用到小丸工具箱，小丸工具箱又沒有Linux version。 （~~wine~~）

後來想想小丸底層也是用的ffmpeg，不如直接命令行翻譯強上。
<!--more-->
## 查找小丸底層命令

在Windows系統盤``HOST_WIN10/Program Files (x86)/MarukoToolbox/logs/``搜出來一份小丸的log文件，可在log中找到小丸的底層調用：

![](/asset/images/技术/wan/00.png)

> "C:\Program Files (x86)\MarukoToolbox\tools\ffmpeg.exe" -i H:\201-5.mp4 -vn -sn -c:a copy -y -map 0:a :0 "C: \Program Files (x86)\MarukoToolbox\temp\201-5_atemp.aac"

第一個命令是用ffmpeg抽取視頻的音頻（這個是這批素材的音頻問題，需要單獨抽離出音頻）

> "C:\Program Files (x86)\MarukoToolbox\tools\x264_32-8bit.exe" --crf 10 --preset 8 -I 250 -r 4 -b 3 --me umh -i 1 --scenecut 60 - f 1:1 --qcomp 0.5 --psy-rd 0.3:0 --aq-mode 2 --aq-strength 0.8 --vf subtitles --sub "H:\201-5.srt" -o "C: \Program Files (x86)\MarukoToolbox\temp\201-5_vtemp.mp4" "H:\201-5.mp4"

第二個是調用x264工具進行字幕編碼，輸出視頻，指定像素比、碼率、壓制方式等等

> "C:\Program Files (x86)\MarukoToolbox\tools\mp4box.exe" -add "C:\Program Files (x86)\MarukoToolbox\temp\201-5_vtemp.mp4#trackID=1:name=" -add "C:\Program Files (x86)\MarukoToolbox\temp\201-5_atemp.aac#trackID=1:name=" -new "C:\Users\Administrator\Desktop\result\201-5_batch.mp4"

第三個是把剛剛的兩步產生的視頻音頻組合

## ffmpeg

在查閱了一些資料後，發現抽離、渲染、組合只需要用ffmpeg就行：

1. 創建基本文件夾：``temp``、``output``

2. 同第一步，抽取音頻，保存到temp中
    ```bash
    ffmpeg -i $1.mp4 -vn -sn -c:a \
        copy -y -map 0:a:0 ./temp/$1_atemp.aac
    # 抽取acc音頻
    ```

3. 因為ffmpeg不支持srt格式，需要轉成ass
    ```bash
    ffmpeg -i $1.mp3-字幕.srt ./temp/$1.ass
    # 轉換字幕格式
    #（帶“.mp3-字幕”是抽音軌識別後科大迅飛自動命名的）
    ```

4. 將抽取的音頻+字幕+音頻丟進去壓制
    ```bash
    ffmpeg -i $1.mp4 -i temp/$1_atemp.aac \
        -vcodec libx264 \ # 指定編碼器
        -deinterlace \ # 指定逐行掃描
        -crf 10 \ # CRF速率控制方法
                                # 0為無損，18為視覺無損，
                                # 預設為23，上限為51
        -preset 8 \ # 指定渲染預設
                                # 有10個速度與質量互扼的預設
                                # veryslow（第二慢） 為 16
                                # 通常指定1～6
        -qcomp 0.5 \ # 指定VBR壓縮
        -psy-rd 0.3:0 \ # 降低psy算法的工作量
        -aq-mode 2 \ # 彈性量化模式 指定自動變化
        -aq-strength 0.8 \ # 彈性量化強度降低
        -vf "ass=temp/$1.ass" # 指定過濾器為字幕
        output/$1_rend.mp4 # 指定輸出視頻位置
    ```

![](/asset/images/技术/wan/01.png)

可以運行，輸出也是正確的，十六核滿爆輸出

![](/asset/images/技术/wan/02.png)


附上[腳本文件](/asset/files/ffmpeg.sh)

感謝燦傑大佬給了我多一篇博客的機會

---
參考資料

1. [h264編碼參數](https://www.jianshu.com/p/b46a33dd958d)

2. [FFMPEG使用參數詳解](https://zhuanlan.zhihu.com/p/31674583)

3. [wiki FFmpeg](http://wiki.webmproject.org/ffmpeg)

4. [使用FFmpeg將字幕文件集成到視頻文件](https://www.yaosansi.com/post/ffmpeg-burn-subtitles-into-video/)