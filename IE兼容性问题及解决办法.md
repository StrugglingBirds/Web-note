### PIE使用方法
实际上是指的是一个名为pie的htc文件，即pie.htc，使用CSS的behavior行为，可以调用此文件，然后让IE也能实现一些常见的 CSS3效果，如圆角(border-radius)，盒阴影(box-shadow)，背景渐变(gradient)，多图片背景(multiple background images)。
下载地址：https://github.com/lojjic/PIE/downloads
##### 支持的主要CSS3属性：
- 1.border-radius圆角
CSS代码如下：
 ```
 .pie_radius{
   width:250px;
   height:250px;
   background-color:#34538b;
   -moz-border-radius:10px;
   -webkit-border-radius:10px;
   border-radius:10px;
   behavior:url(pie.htc);
 }
 ```
html代码如下：
```
<div class="pie_radius"></div>
```
- 2.box-shadow 盒阴影
CSS代码如下：
```
.pie_box_shadow{
   width:250px;
   height:250px;
   background-color:#34538b;
   -moz-box-shadow:1px 3px 3px #666;
   -webkit-box-shadow:1px 3px 3px #666;
   box-shadow:1px 3px 3px #666;
   behavior:url(pie.htc);
 }
 ```
 html代码如下：
 ```
 <div class="pie_box_shadow"></div>
 ```
 - 3.gradient渐变
 CSS代码如下：
 ```
 .pie_gradient{
   width:250px;
   height:250px;
   background-color:#9F9;
   background:-webkit-gradient(linear, 0 0, 0 bottom, from(#9F9), to(#393));
   background:-moz-linear-gradient(#9F9, #393);      
   -pie-background:linear-gradient(#9F9, #393);
   behavior:url(pie.htc);  
 }
 ```
 html代码如下：
 ```
 <div class="pie_gradient"></div>
 ```
 - 4.background多背景图
 CSS代码如下:
 ```
 .pie_background{
   width:250px;
   height:250px;
   background:url(./img1.png) no-repeat right top, url(./img2.png) no-repeat left bottom;
   background-size: 20px 30px, 40px 50px;
 }
 ```
 html代码如下:
 ```
 <div class="pie_background"></div>
 ```
