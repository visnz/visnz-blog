---
title: 相冊
date: 2019-10-17 16:44:40
type: "album"
---

<head>
    <link rel="stylesheet" href="css/lightgallery.css">
</head>
<body>
    <script src="js/lightgallery.min.js"></script>
    <!-- lightgallery plugins -->
    <script src="js/lg-thumbnail.min.js"></script>
    <script src="js/lg-fullscreen.min.js"></script>
</body>
<style type="text/css">
#lightgallery{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
#lightgallery a{
    border-bottom: 0px;
    height: 200px;
}
#lightgallery img{
    width: 200px;
    height: 200px;
    object-fit: cover;
    display: inline;
    margin-left: 0px;
    margin-right: 0px;
}
#lightgallery video{
    width: 200px;
    height: 200px;
    object-fit: cover;
    display: inline;
    margin-left: 0px;
    margin-right: 0px;
}
</style>
<script type="text/javascript">
var size=3
function setSize(){
    var a
    switch(size){
        case 6:
            a = "800px"
            break;
        case 5:
            a = "400px"
            break;
        case 4:
            a = "300px"
            break;
        case 3:
            a = "200px"
            break;
        case 2:
            a = "150px"
            break;
        case 1:
            a = "100px"
            break;
        case 0:
            a = "50px"
            break;
        default:
            a = "200px"
            size=3
            break;
    }
    document.querySelectorAll("#lightgallery a").forEach((i)=>i.style="height: "+a)
    document.querySelectorAll("#lightgallery img").forEach((i)=>i.style="height: "+a+";width: "+a+";")
    document.querySelectorAll("#lightgallery video").forEach((i)=>i.style="height: "+a+";width: "+a+";")
}
</script>
<div style="margin: 20px auto;text-align: center;">
    <a onclick='size+=1;setSize()'>擴大</a>
    <a onclick='size-=1;setSize()'>縮小</a>
</div>
<div id="lightgallery">
    <img src="/asset/album/phy/SHF_9981.jpg">
    <img src="/asset/album/3D/piano2.jpg">
    <video src="/asset/videos/aep02/end.mp4" controls="controls"></video>
    <img src="/asset/videos/aep02/title.png">
    <img src="/asset/videos/c4dp07/效果图.jpg">
    <video src="/asset/videos/c4dp06/Mondrian.mp4" controls="controls"></video>
    <img src="/asset/videos/c4dp06/Mondrian.jpg">
    <img src="/asset/videos/c4dp05/pokemon1.jpg">
    <img src="/asset/videos/c4dp05/pokemon2.jpg">
    <img src="/asset/videos/c4dp05/pokemon3.jpg">
    <img src="/asset/videos/c4dp05/pokemon_0004.jpg">
    <img src="/asset/videos/c4dp05/pokemon_0005.jpg">
    <img src="/asset/videos/c4dp04/adobe-part1.jpg">
    <img src="/asset/videos/c4dp04/adobe-part2.jpg">
    <img src="/asset/videos/c4dp04/adobe-part3.jpg">
    <img src="/asset/videos/c4dp04/adobe-part4.jpg">
    <img src="/asset/videos/c4dp04/adobe-part5.jpg">
    <img src="/asset/videos/c4dp04/adobe-part6.jpg">
    <img src="/asset/videos/c4dp04/adobe.gif">
    <img src="/asset/videos/c4dp04/adobe.jpg">
    <img src="/asset/videos/c4dp03/球球.jpg">
    <img src="/asset/videos/c4dp02/arm.jpg">
    <video src="/asset/videos/aep01/mankind.mp4" controls="controls"></video>
    <img src="/asset/videos/aep01/mankind.png">
    <img src="/asset/videos/c4dp01/ball.jpg">
    <img src="/asset/images/大学/HEC_4029.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3967s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3954s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3953s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3945s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3924s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3931s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3918s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3907s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3903s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3896s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3878s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3875s.jpg">
    <img src="/asset/images/毕业后/hikee2/HEC_3862s.jpg">
    <img src="/asset/images/大学/HEC_3830.jpg">
    <img src="/asset/images/大学/HEC_3839.jpg">
    <img src="/asset/images/毕业后/food/HEC_3816.jpg">
    <img src="/asset/images/毕业后/food/HEC_3820.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7733.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7729.jpg">
    <img src="/asset/images/大学/珠海/JAP_7723.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7718.jpg">
    <img src="/asset/images/大学/珠海/JAP_7709.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7708.jpg">
    <img src="/asset/images/大学/珠海/JAP_7690.jpg">
    <img src="/asset/images/大学/珠海/JAP_7686.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7681-编辑.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7665.jpg">
    <img src="/asset/images/大学/珠海/JAP_7658.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7653.jpg">
    <img src="/asset/images/大学/珠海/S2JAP_7641.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7632.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7628.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7625.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7598.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7585-编辑.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7581.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7513.jpg">
    <img src="/asset/images/大学/珠海/S1JAP_7501.jpg">
    <img src="/asset/images/大学/珠海/JAP_7497.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5717.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5709.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5664.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5652.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5633.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5582_01.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5538_01.jpg">
    <img src="/asset/images/大学/红砖厂hikee/JAP_5534_01.jpg">
    <img src="/asset/images/大学/hongkong/hkxma/photo1.jpg">
    <img src="/asset/images/大学/hongkong/hkxma/photo2.jpg">
    <img src="/asset/images/大学/hongkong/JAP_3794.jpg">
    <img src="/asset/images/大学/hongkong/JAP_3783.jpg">
    <img src="/asset/images/大学/hongkong/JAP_3771.jpg">
    <img src="/asset/images/大学/hongkong/JAP_3768.jpg">
    <img src="/asset/images/大学/沙面33/CIMG_4186.jpg">
    <img src="/asset/images/大学/沙面33/CIMG_4168.jpg">
    <img src="/asset/images/大学/沙面33/CIMG_4160.jpg">
    <img src="/asset/images/大学/沙面33/CIMG_4143.jpg">
    <img src="/asset/images/大学/沙面33/AIMG_4083.jpg">
    <img src="/asset/images/大学/沙面33/DIMG_4017.jpg">
    <img src="/asset/images/大学/沙面33/DIMG_4014.jpg">
    <img src="/asset/images/大学/沙面33/BIMG_3943.jpg">
    <img src="/asset/images/大学/沙面33/AIMG_3910.jpg">
    <img src="/asset/images/大学/红砖厂/IMG_3872.jpg">
    <img src="/asset/images/大学/红砖厂/IMG_3882.jpg">
    <img src="/asset/images/大学/红砖厂/IMG_3883.jpg">
    <img src="/asset/images/大学/红砖厂/IMG_3884.jpg">
    <img src="/asset/images/大学/红砖厂/IMG_3886.jpg">
    <img src="/asset/images/大学/红砖厂/IMG_3888.jpg">
    <img src="/asset/images/大学/nihon/icon.png">
    <img src="/asset/images/大学/nihon/pic14.jpg">
    <img src="/asset/images/大学/nihon/pic23.jpg">
    <img src="/asset/images/大学/nihon/pic21.jpg">
    <img src="/asset/images/大学/nihon/pic19.jpg">
    <img src="/asset/images/大学/nihon/pic22.jpg">
    <img src="/asset/images/大学/nihon/pic08.jpg">
    <img src="/asset/images/大学/nihon/JAP_1490s2.jpg">
    <img src="/asset/images/大学/nihon/IMG_6716.JPG">
    <img src="/asset/images/大学/nihon/IMG_6763.JPG">
    <img src="/asset/images/大学/nihon/pic15.jpg">
    <img src="/asset/images/大学/nihon/pic27.jpg">
    <img src="/asset/images/大学/nihon/IMG_6750.JPG">
    <img src="/asset/images/大学/nihon/IMG_6319 （已编辑）.JPG">
    <img src="/asset/images/大学/nihon/IMG_6751.JPG">
    <img src="/asset/images/大学/nihon/IMG_6752.JPG">
    <img src="/asset/images/大学/nihon/IMG_6746.JPG">
    <img src="/asset/images/大学/nihon/IMG_6747.JPG">
    <img src="/asset/images/大学/cat/FAS_0593s.jpg">
    <img src="/asset/images/大学/cat/FAS_0591.jpg">
    <img src="/asset/images/大学/cat/FAS_0589s.jpg">
    <img src="/asset/images/大学/cat/FAS_0585s.jpg">
    <img src="/asset/images/大学/canton/FAS_0530.jpg">
    <img src="/asset/images/大学/canton/IMG_5342.JPG">
    <img src="/asset/images/大学/canton/FAS_0511s.jpg">
    <img src="/asset/images/大学/canton/IMG_5225.JPG">
    <img src="/asset/images/大学/红砖厂33/flower.jpg">
    <img src="/asset/images/大学/红砖厂33/cat.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_2204_8.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_2173_8.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_2138_8.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_2065_8.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_2053_8.jpg">
    <img src="/asset/images/大学/红砖厂33/IMG_5104.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_2010_8.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_1909_8.jpg">
    <img src="/asset/images/大学/红砖厂33/FAS_1902_8.jpg">
    <img src="/asset/images/大学/分手散片/DSC_2663s.jpg">
    <img src="/asset/images/大学/分手散片/IMG_4754.JPG">
    <img src="/asset/images/大学/大学早期/DSC_9405ss.jpg">
    <img src="/asset/images/大学/大学早期/DSC_2365.jpg">
    <img src="/asset/images/大学/梓麟饼干/DSC_2359sA.jpg">
    <img src="/asset/images/大学/梓麟饼干/DSC_2364sA.jpg">
    <img src="/asset/images/大学/梓麟饼干/DSC_2346ss.jpg">
    <img src="/asset/images/大学/梓麟饼干/DSC_2342s.jpg">
    <img src="/asset/images/大学/梓麟饼干/DSC_2337ss.jpg">
    <img src="/asset/images/大学/梓麟饼干/DSC_2335ss.jpg">
    <img src="/asset/images/大学/大学早期/DSC_9311.JPG">
    <img src="/asset/images/大学/大学早期/IMG_2123.JPG">
    <img src="/asset/images/大学/大学早期/IMG_2091.JPG">
    <img src="/asset/images/大学/学生会/假如/IMG_6511.jpg">
    <img src="/asset/images/大学/学生会/假如/IMG_6452.jpg">
    <img src="/asset/images/大学/学生会/假如/DSC_8073.jpg">
    <img src="/asset/images/大学/学生会/假如/DSC_8067.jpg">
    <img src="/asset/images/大学/学生会/假如/DSC_8039.jpg">
    <img src="/asset/images/大学/学生会/假如/DSC_8030.jpg">
    <img src="/asset/images/大学/大学早期/DSC_5876.jpg">
    <img src="/asset/images/大学/大学早期/DSC_5837s.jpg">
    <img src="/asset/images/大学/学生会/兽爷/baDSC_5873.jpg">
    <img src="/asset/images/大学/学生会/兽爷/baDSC_5834s.jpg">
    <img src="/asset/images/大学/学生会/兽爷/baDSC_5832.jpg">
    <img src="/asset/images/大学/学生会/兽爷/baDSC_5821.jpg">
    <img src="/asset/images/大学/学生会/兽爷/baDSC_5815.jpg">
    <img src="/asset/images/大学/大学早期/DSC_5676s.jpg">
    <img src="/asset/images/大学/大学早期/aDSC_5199.jpg">
    <img src="/asset/images/大学/胶片/000029.jpg">
    <img src="/asset/images/大学/胶片/000016.jpg">
    <img src="/asset/images/大学/胶片/000055.jpg">
    <img src="/asset/images/大学/胶片/000038.jpg">
    <img src="/asset/images/大学/胶片/000026.jpg">
    <img src="/asset/images/大学/胶片/000022.JPG">
    <img src="/asset/images/大学/胶片/hIMG_1125.JPG">
    <img src="/asset/images/大学/胶片/hIMG_1129.JPG">
    <img src="/asset/images/大学/胶片/IMG_1124.JPG">
    <img src="/asset/images/大学/胶片/000005.JPG">
    <img src="/asset/images/大学/大学早期/a4864.jpg">
    <img src="/asset/images/大学/大学早期/DSC_4794.JPG">
    <img src="/asset/images/大学/大学早期/DSC_4789.JPG">
    <img src="/asset/images/大学/Enc/aDSC_2451.jpg">
    <img src="/asset/images/大学/Enc/aDSC_2450.jpg">
    <img src="/asset/images/大学/Enc/aDSC_2443.jpg">
    <img src="/asset/images/大学/Enc/aDSC_2436.jpg">
    <img src="/asset/images/大学/Enc/aDSC_24282.jpg">
    <img src="/asset/images/大学/Enc/aDSC_2419.jpg">
    <img src="/asset/images/高中/散片/6.jpg">
    <img src="/asset/images/高中/散片/5.jpg">
    <img src="/asset/images/高中/散片/baDSC_6180.jpg">
    <img src="/asset/images/高中/散片/DSC_4362.jpg">
    <img src="/asset/images/高中/甜甜圈/DSC_4923_副本.jpg">
    <img src="/asset/images/高中/甜甜圈/DSC_4927_副本.jpg">
    <img src="/asset/images/高中/甜甜圈/DSC_4930_副本.jpg">
</div>
<script>
    lightGallery(document.getElementById('lightgallery'));
</script>
<!--more-->
