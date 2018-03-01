### PIE使用方法
实际上是指的是一个名为pie的htc文件，即pie.htc，使用CSS的behavior行为，可以调用此文件，然后让IE也能实现一些常见的 CSS3效果，如圆角(border-radius)，盒阴影(box-shadow)，背景渐变(gradient)，多图片背景(multiple background images)。
下载地址：https://github.com/lojjic/PIE/downloads
##### 支持的主要CSS3属性：
- 1.border-radius圆角<br>
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
- 2.box-shadow 盒阴影<br>
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
 - 3.gradient渐变<br>
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
 - 4.background多背景图<br>
 CSS代码如下:
 ```
 .pie_background{
   width:250px;
   height:250px;
   background:url(./img1.png) no-repeat right top, url(./img2.png) no-repeat left bottom;
   background-size: 20px 30px, 40px 50px;
   behavior:url(pie.htc);
 }
 ```
 html代码如下:
 ```
 <div class="pie_background"></div>
 ```
以上为PIE1.0.0的使用方法
如若使用的PIE2.0.0,需引入对应版本的PIE.ie678.js或PIE.ie9.js
-  5.问题说明：
> A. IE下这些CSS3效果实现是借助于VML，由VML绘制圆角或是投影效果的容器元素，然后这个容器元素作为目标元素的后兄弟节点插入，如果目标元素position:absolute 或是 position:relative，则这个css3-container元素将会设置与之一样的z-index值，在DOM tree中，同级的元素总是后面的覆盖前面的，所以这样就实现了覆盖，又避免了可能有其他元素正好插入其中。所 以，问题来了，如果目前元素的position属性为static，也就是默认属性，则z-index属性是没有用的，无覆盖可言，所以此时IE浏览器下 CSS3的渲染是不会成功的。要解决也很简单，设置目标元素position:relative或是设置祖先元素position:relative并赋 予一个z-index值（不可为-1）。

> B. IE浏览器的behavior 属性是相对于HTML文档而言的，与CSS其他的属性不一样，不是相对于CSS文档而言的。这使得使用pie.htc文件不怎么方变。如果绝对路径于根目 录，则CSS文件不方便移动；如果相对路径与HTML文档，则pie.htc文件在不同HTML页面见的重用性大大降低。同时，诸如border- image后面的URL属性路径也不好处理。 

> C. 使用PIE实现IE下的CSS3渲染（其他方法也是一样），只能使用缩写的形式，例如圆角效果，我们可以设置border-top-left-radius表示左上圆角，但是PIE确实不支持这种写法的，只能是老老实实的缩写。

> D. 要想让IE浏览器支持htc文件，需要一个有着”text/x-component” 字样的content-type 头部，否则，会忽视behavior。绝大数web服务器提供了正确的content-type，但是还有一部分则有问题。

> E. 由于某种原因，您无法修改服务器配置（例如公用主机，或是空间服务商提供的服务器），您可以用一个PHP文件来间接调用htc文件。
<?php  header( 'Content-type: text/x-component' );  include( 'pie.htc' );  ?>
通过PHP文件来增加一个含有“text/x-component”字样的Content-type头，同时调用pie.htc文件。需要将pie.php和pie.htc放在同一个文件夹目录下，同时CSS中的behavior写法应该是：
behavior: url(pie.php);
