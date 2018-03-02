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
#### 2.计算属性
- 计算属性用于非频繁更新的需要逻辑处理之后获取结果的组件数据
- 计算属性有getter和setter，默认方法为getter
- get方法为获取计算属性的值时要执行的逻辑代码，数据结果需要return出来
- set方法为更新计算属性的值时要执行的逻辑代码，方法无需return
- 计算属性只有在setter执行，即更新计算属性的值发生变化时，才会更新数据，简单来说，set方法执行后会自动执行get方法

(1)代码示例
```
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```
#### 3.Vuex的使用方法
###### 安装方法(webpack中Vuex安装)
(1)使用npm安装Vuex依赖
```
npm install vuex --save-dev
```
(2)在main.js中全局引入
```
  import App from './App'
  import Vue from 'vue'   //引入Vue
  import Vuex from 'vuex' //引入Vuex
  import router from './router' //引入router
  Vue.use(Vuex)
  
  /*创建状态管理对象*/
  const store = new Vuex.Store({
    state: {
      count: ''
    },
    mutations: {
      add (state) {
        state.count++
      },
      reduce (state) {
        state.count--
      }
    }
  })
  
  /*创建Vue实例，将Vuex的store全局引入*/
  const vm = new Vue({
    el: '#app',
    template: '<App/>',
    components: { App }
    store,
    router
  })
```
(3)在App组件中使用
```
<template>
  <div id="app">
    <button @click="$store.commit('add')">+</button>
    <span>{{ $store.state.count }}</span>
    <button @click="$store.commit('reduce')">-</button>
  </div>
</template>
<script>
  export default {
    name: 'app'
  }
</script>
```
