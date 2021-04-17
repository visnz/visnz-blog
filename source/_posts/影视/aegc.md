---
title: Ae脚本开发杂记：全局同步属性控制器v2.1.0 
tags:
  - "影視"
  - Ae
  - 开发
categories: "影視"
date: 2020-02-23
updated: 2020-02-25
---
---
# 提要
本文大概记录了脚本开发前后想法，以及开发过程总结。[Github地址，包含源码](https://github.com/visnz/AeGlobalController)


![成品](/asset/images/技术/aegc/panel.png)
![示意图](/asset/images/技术/aegc/example.gif)

# 前言

在打包工程时候出现跨合成引用的丢失、合成内有多个变量需要统一修改、全局合成需要一个可以控制的全局数据结构来指挥，比如用于**方案的打包**、色彩的选择，大小变化、表达式系数、合成内外抽离控制等等。

另外创建控制器也较为繁琐，“创建”后需要打开当前内容、点开控制器、链接，创建一个一键式按钮。判断当前属性类型直接创建、同步

<!--more-->
# 设计大览
一开始的想法设计是：

```
一个合成，专门放置控制器，外部数据引用这里
```

在实站过程中，发现基本结构没问题，但是每次要链接过于繁琐，而且调整的话，得过去调整再回来看效果，效率较低。

后来改成
```
每个合成都创建一个控制器，每次更新控制器的时候，同步到所有控制器。
```

再加上后台跑监听函数自动同步，用来解决对调整的实时反馈

# 具体设计
1. 库：包含了之前自己写的一些操作函数
2. 模式设计：Debug模式、AlertMsg提醒模式、AutoSync自动同步模式
3. 页面函数，创建页面内容交互（按钮事件等）
4. 同步板块：
    1. 暂存原型
    2. 记录函数（更新原型）
    3. 判断函数（判断是否更新）
    4. 同步函数
    5. 后台监听（自动同步）
5. 给所有合成创建控制器的函数
6. 按钮事件：
    1. 检查已选择属性
    2. 在控制器创建对应属性并链接
7. 其他：设置undo组方便回滚

# 代码（全注释版）
```js
UI(this);
var alertMsg=true   // AlertMsg提醒模式，打开时操作会有alert提示
var autoSync=false  // AutoSync自动同步模式，打开时每隔一段时间进行检查更新
var debugMode=false // 纠错模式，打开时会出现运行时提示

function UI(object){
    var myPalette = (object instanceof Panel)?object : new Window("palette","控制器2.0", undefined, {resizeable: true})
    var content=""+
    "group {orientation:'column', alignment:['fill','fill'], spacing:5, "+
        "mainGroup: Group {text:'控制抽取', alignment:['fill','top'], orientation:'row', spacing:5 ,"+
            "button0: Button {text:'2D点', alignment:['fill','top'], preferredSize:[45,25]},"+
            "button1: Button {text:'3D点', alignment:['fill','top'], preferredSize:[45,25]},"+
            "button2: Button {text:'复选', alignment:['fill','top'], preferredSize:[45,25]},"+
            "button3: Button {text:'滑块', alignment:['fill','top'], preferredSize:[45,25]},"+
            "button4: Button {text:'角度', alignment:['fill','top'], preferredSize:[45,25]},"+
            "button5: Button {text:'颜色', alignment:['fill','top'], preferredSize:[45,25]}"+
        "},"+
        "secondGroup: Group {text:'功能', alignment:['fill','top'], orientation:'column', spacing:5 ,"+
            "line1: Group {text:'功能', alignment:['fill','top'], orientation:'row', spacing:5 ,"+
                "button6: Button {text:'全部创建', alignment:['fill','top'], preferredSize:[150,25]},"+
                "button8: Checkbox {text:'弹出提示', alignment:['fill','top'], preferredSize:[50,25]},"+
            "},"+
            "line2: Group {text:'功能', alignment:['fill','top'], orientation:'row', spacing:5 ,"+
                "button7: Button {text:'同步当前', alignment:['fill','top'], preferredSize:[150,25]},"+
                "button9: Checkbox {text:'自动同步', alignment:['fill','top'], preferredSize:[50,25]},"+
            "},"+
        "},"+

    "}"
    // 创建面板
    myPalette.grp = myPalette.add(content);
    myPalette.grp.add("statictext",undefined,"Made By 水桶")
    myPalette.grp.add("statictext",undefined,"更多：v.guediao.top")
    // 链接事件
    myPalette.grp.secondGroup.line1.button6.onClick=createAll
    myPalette.grp.secondGroup.line2.button7.onClick=sync
    myPalette.grp.secondGroup.line1.button8.value=true
    myPalette.grp.secondGroup.line2.button9.value=false
    myPalette.grp.secondGroup.line1.button8.onClick=changeAlertMsg
    myPalette.grp.secondGroup.line2.button9.onClick=changeAutoSync
    myPalette.grp.mainGroup.button0.onClick=create2DPoint
    myPalette.grp.mainGroup.button1.onClick=create3DPoint
    myPalette.grp.mainGroup.button2.onClick=createCheckbox
    myPalette.grp.mainGroup.button3.onClick=createSlider
    myPalette.grp.mainGroup.button4.onClick=createAngle
    myPalette.grp.mainGroup.button5.onClick=createColor
    myPalette.layout.layout(true);
    // 设置画面显示
    myPalette.layout.resize();
    // 设置完自适应调整
    myPalette.onResizing = myPalette.onResize = function() {this.layout.resize();};
    // 设置调整函数
    if (myPalette != null && myPalette instanceof Window) {
        myPalette.center()
        myPalette.show();
    }
}

function create2DPoint(){
    if(app.project.activeItem.selectedLayers[0].name=="controlLayer")return
    // 如果不存在控制图层则返回
    app.beginUndoGroup("create Point");
    // 创建undo组
    var properties=getSelectedPropertie()
    var controlLayer=app.project.activeItem.layers.byName("controlLayer")
    if(properties.expression!=""||!properties.canSetExpression){if(alertMsg)alert("无法创建或已有表达式");return;}
    // 已有表达式的情况下防止碰撞
    if(properties.value.length==3||properties.value.length==2){
        controlLayer.Effects.addProperty("点控制")("点").setValue([properties.value[0],properties.value[1]]);
        // 属性值匹配情况下，创建控制器，修改为当前值
        var indexName=getCurProperNameFully()
        controlLayer("Effects")("点控制").name=indexName
        // 属性名生成
        properties.expression='thisComp.layer("controlLayer").effect("'+indexName+'")("点")'
        // 修改表达式
        if(alertMsg)alert("创建完毕")
    }
    app.endUndoGroup();
}
function create3DPoint(){...}
function createCheckbox(){...}
function createSlider(){...}
function createAngle(){...}
function createColor(){...}
// 以上函数都是类似的逻辑

function changeAlertMsg(){
    alertMsg=!alertMsg
}
function changeAutoSync(){...}
// 同上

var oldProper
// 创建暂存原型

function record(){
    // 记录函数，用于记录当前激活的效果器的属性值
    // 配合检查是否有更新
    if(debugMode)alert("record()")
    var propers=[]
    if(!app.project.activeItem)return undefined
    var count=app.project.activeItem.layers.byName("controlLayer")("Effects").numProperties
    // 获取控制器属性的数量，较新版本不允许catch获取临界值
    for(var i=1;i<=count;i++){
        // 遍历尝试获取效果器
        try{
            var eff=app.project.activeItem.layers.byName("controlLayer").Effects(i)
        }catch(e){
            break
        }
        var value=eff(effectProperType(eff)).value
        propers.push(value)
        // 将属性值推入组
    }
    return propers
}

function hasChanged(){
    // 检查当前激活控制器与原型差别，有不同则触发更新 
    if(!app.project.activeItem)return undefined
    if(!app.project.activeItem.layers.byName("controlLayer"))return undefined
    var count=app.project.activeItem.layers.byName("controlLayer")("Effects").numProperties
    // 获取控制器属性的数量，较新版本不允许catch获取临界值
    if(!oldProper)return false
    // 暂存原型不存在则返回
    if(count!=oldProper.length)return true
    // 属性数量发生变化，触发更新
    for(var i=1;i<=count;i++){
        // 遍历尝试获取效果器
        try{
            var eff=app.project.activeItem.layers.byName("controlLayer").Effects(i)
        }catch(e){
            break
        }
        var value=eff(effectProperType(eff)).value
        if(value.toString()!=oldProper[i-1].toString()){
            // 逐个比较直，如果不一样则触发更新
            return true
        }
    }
    return false
}

function sync(){
    // 同步函数
    if(debugMode)alert("sync()")
    if(!app.project.activeItem)return
    if(!app.project.activeItem.layers.byName("controlLayer"))return
    app.beginUndoGroup("Sync controller config");
    var activeViewer=app.activeViewer 
    // 记录当前活跃的窗口
    var createTimes=0 
    // 统计更新的合成数
    var comps=getControlComps()
    // 获取全部合成
    var curComp=app.project.activeItem
    for(var i=0;i<comps.length;i++){
        if(comps[i]!=curComp){
        comps[i].layers.byName("controlLayer").remove()
        app.project.activeItem.layers.byName("controlLayer").copyToComp(comps[i])
        // 移除旧控制器并添加新控制器
        createTimes++
        }
    }
    if(alertMsg)alert("同步到"+createTimes+"个")
    activeViewer.setActive() 
    // 激活原来活跃的面板
    oldProper=record()
    // 更新原型
    app.endUndoGroup();
}

app.scheduleTask('if(autoSync&&hasChanged())sync()',1000,true)
// 构建定时执行事件，完成后台同步

function createAll(){
    // 创建所有合成控制器
    app.beginUndoGroup("create All Comp Controller");
    var comps=getControlComps()
    var createTimes=0
    for(var i=0;i<comps.length;i++){
        var controlLayer=comps[i].layers.byName("controlLayer")
        if(!controlLayer){
            // 遍历添加
            controlLayer=comps[i].layers.addNull()
            controlLayer.name="controlLayer"
            createTimes++
        }
    }
    if(alertMsg)alert("全部创建完毕，共创建"+createTimes+"个")
    app.endUndoGroup();
}


//===lib===//

// 获取所有合成对象
function getControlComps(){
    var comps=[]
    for(var i=1;i<=app.project.items.length;i++){
        if(app.project.items[i] instanceof CompItem){
            comps.push(app.project.items[i])
        }
    }
    return comps
}

```
注：以上代码不是可运行代码，可直接前往[Github地址](https://github.com/visnz/AeGlobalController)获取。

