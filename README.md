# Web-note
本人在web前端这方面的一些学习笔记及分享一些前端资源
>  1.git官网[学习资料](https://git-scm.com/book/zh/v2) <br>
>  2.关于IE8及以下IE版本对媒体查询@media的兼容处理需在HEAD标签中引入[respond.js](https://github.com/StrugglingBirds/Web-note/blob/master/respond.js) <br>
>  3.jquery中的animate无法操作CSS3中的图形变换属性，例如：transform中的属性（rotate、scale、translate...) <br>
>  4.zoom与CSS3中的scale的区别： <br>
      - zoom的缩放是相对于左上角的；而scale默认是居中缩放； <br>
      - zoom的缩放改变了元素占据的空间大小；而scale的缩放占据的原始尺寸不变，页面布局不会发生变化； <br>
      - zoom和scale对元素的渲染计算方法可能有差异（需要自己动手，用高清图，仔细去看其中的区别）。 <br>
      - 对文字的缩放规则不一致。zoom缩放依然受限于最小12像素中文大小限制；而scale就是纯粹的对图形进行比例控制，文字50%原来尺寸。 <br>
