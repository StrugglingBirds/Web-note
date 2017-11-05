## gulp常用功能
- 1、根据package.json文件安装依赖 命令：**cnpm install**
- 2、gulp-jshint 对JavaScript代码进行语法检查
- 2.1、安装时可能出现的问题：
##### jshint的安装语法：
  ` npm install gulp-jshint --save-dev`
##### 安装报错：
  ` Error: Cannot find module 'jshint/src/cli'`
##### 解决方法：
  ` npm install jshint gulp-jshint --save-dev`
- 3、gulp-concat 同一类型的文件合并(javascript、css)
- 4、gulp-autoprefixer CSS编译自动添加浏览器适配的-webkit-等兼容性样式前缀
- 5、gulp-uglify 压缩JavaScript代码
- 6、gulp-minify-css 压缩CSS代码
- 7、gulp-imagemin 压缩图片
- 8、gulp-htmlmin 压缩HTML代码
- 9、gulp-rename 文件重命名
## gulp资源分享
- 1、[gulp详细入门教程](http://www.ydcss.com/archives/18#lesson1)**
- 2、[gulpfile.js语法教程及依赖安装教程](http://www.cnblogs.com/2050/p/4198792.html)
