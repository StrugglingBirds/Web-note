#### Vue知识点理解及使用方法
##### 1.异步组件
- 表现：异步组件在页面加载时，只有在需要加载此组件时才会按需加载组件
- 优点：优化初次加载页面时的性能
- 缺点：Browserify在默认情况下不支持
(1) 在非webpack打包脚手架环境下的使用方法
``` 
<html>
<head>
  <title>Async Component test</title>
</head>
<body>

  <div id="app">
    <router-link to="/home">/home</router-link>
    <router-link to="/about">/about</router-link>
    <router-view></router-view>
  </div>

  <script src="https://unpkg.com/vue/dist/vue.js"></script>
  <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
  <script>
    function load(componentName, path) {
      return new Promise(function(resolve, reject) {
        var script = document.createElement('script');
        script.src = path;
        script.async = true;
        script.onload = function() {
          var component = Vue.component(componentName);
          if (component) {
            resolve(component);
          } else {
            reject();
          }
        };
        script.onerror = reject;
        document.body.appendChild(script);
      });
    }
    var router = new VueRouter({
      routes: [
        {
          path: '/',
          redirect:'/home'
        },
        {
          path: '/home',
          component: {
            template: '<div>Home page</div>'
          },
        },
        {
          path: '/about',
          component: function(resolve, reject) {
            load('about', 'about.js').then(resolve, reject);
          }
        }
      ]
    });
    var app = new Vue({
      el: '#app',
      router: router,
    });
  </script>

</body>
</html>
```
(2) 在webpack的环境下
```
//test.vue的部分
<script>
    import Vue from 'vue'

    //关键是以下这部分代码
    //需要将引入的异步组件，赋值给变量searchSearch
    //然后在下方components对象里，将变量正常添加进去，就可以使用异步组件了
    //第一个参数是组件名，第二个是异步引入的方法
    const searchSearch = Vue.component('searchSearch', function (resolve) {
        require(['./service-search.vue'], resolve)
    })

    export default{
        data(){
            return {}
        },
        methods: {},
        components: {
            searchSearch: searchSearch
        }
    }
</script>
```
更简单的方法
```
<script>
    export default{
        data(){
            return {}
        },
        methods: {},
        components: {
            searchSearch: function (resolve) {
                //异步组件写法
                require(['./service-search.vue'], resolve)
            }
        }
    }
</script>
```
