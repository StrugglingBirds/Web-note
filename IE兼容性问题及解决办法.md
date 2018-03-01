### PIE使用方法
实际上是指的是一个名为pie的htc文件，即pie.htc，使用CSS的behavior行为，可以调用此文件，然后让IE也能实现一些常见的 CSS3效果，如圆角(border-radius)，盒阴影(box-shadow)，背景渐变(gradient)，多图片背景(multiple background images)。
下载地址：https://github.com/lojjic/PIE/downloads
##### 支持的主要CSS3属性：
- 1.border-radius圆角
   CSS代码如下：
> ```.pie_radius{ width:250px;height:250px;background-color:#34538b;-moz-border-radius:10px;      -webkit-border-radius:10px;border-radius:10px;behavior:url(pie.htc);}```
