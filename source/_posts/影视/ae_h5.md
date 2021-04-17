---
title: AE插件Bodymovin联动lottie-web构建HTML5动画
tags: 
    - Ae
updated: 2020-03-28
date: 2020-03-28
categories: "影視"
---
---
# 前言
<iframe src="https://guediao.top/dev/test.html" style="height: 600px;width: 100%;"></iframe>

[测试成品](https://guediao.top/dev/test.html)

![](/asset/content/ae_h5/示意图.png)
<!--more-->
# 准备工作
[AE插件Bodymovin](https://github.com/bigxixi/bodymovin)(.zxp)，通过[ZXP Installer](https://aescripts.com/learn/zxp-installer/)安装。

[airbub官方文档及 支持的效果](https://airbnb.io/lottie/#/supported-features)

# 步骤

简单制作ae动画使用Bodymovin渲染导出，在html中导入：
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/bodymovin/5.6.6/lottie.min.js"></script>
<div id="animation" style="height: 1000px;"></div>
<script>
    lottie.loadAnimation({
        path:'./data.json',   //json文件路径
        loop:true,
        autoplay:true,
        renderer:'canvas',  //渲染方式，有"html"、"canvas"和"svg"三种
        container:document.getElementById('animation')
    });
    //lottie-web的完整api文档见GitHub项目首页(https://github.com/airbnb/lottie-web)
</script>
```

同目录下放置``data.json``，刚刚简单制作的
```js
{
	"v": "4.6.2","fr": 24,"ip": 0,"op": 82,"w": 1000,"h": 1000,"nm": "合成 1","ddd": 0,
	"assets": [],
	"layers": [{
		"ddd": 0,
		"ind": 1,
		"ty": 1,
		"nm": "红色 纯色 1",
		"ks": {
			"o": {"a": 0,"k": 100},
			"r": {"a": 0,"k": 0},
			"p": {
				"a": 1,
				"k": [{
					"i": {"x": 0.25,"y": 1},
					"o": {"x": 0.8,"y": 0
					},
					"n": "0p25_1_0p8_0",
					"t": 0,
					"s": [0, 500, 0],
					"e": [500, 500, 0],
					"to": [83.3333358764648, 0, 0],
					"ti": [-83.3333358764648, 0, 0]
				}, {
					"t": 24
				}]
			},
			"a": {"a": 0,"k": [100, 100, 0]},
			"s": {"a": 0,"k": [100, 100, 100]
			}
		},
		"ao": 0,"sw": 200,"sh": 200,"sc": "#c42929","ip": 0,"op": 82,"st": 0,"bm": 0,"sr": 1
	}]
}
```

# 参考链接

[动画：从 AE 到 Web](https://aotu.io/notes/2018/03/06/ae2web/index.html)
