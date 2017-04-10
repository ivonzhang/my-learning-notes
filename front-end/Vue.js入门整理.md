## Vue基础 ##
- ### 常用指令 ###
  - 循环v-for
    数组v-for="name in arr" , json格式v-for="name in jason", v-for="(k,v) in json"； {{$index}}  , {{$key}}

  - 事件v-on:click/mouseout/mouseover/...,如： v-on:click="函数"，该指令可以简写为@click="函数"

  - 显示隐藏： v-show="true|false"

  - 事件对象 @click="func($event)", 参数$event相当于js中的event

  - 事件冒泡，阻止冒泡：
    - js的方式：event.cancleBubble = true
    - @click.stop

  - 事件默认行为，阻止默认行为：
    - js的方式： event.preventDefault()
    - contextmenu.prevent

  - 键盘事件：@keydown ，@keyup等等

  - 属性v-bind，如v-bind:src="", 简写:src=""

  - 样式clsaa和style
    - :class="" 或 v-bind:class=""
    - :style="" 或 v-bind:style=""

  - 模板
    - 文本{{msg}}}，指令v-text=""
    - 只输出一次 {{*msg}}
    - html转义输出 {{{msg}}}，指令v-html=""

  - 过滤器：{{msg | filterA}} ，{{msg | filterA, filterB}}

  - 计算属性computed：里面可以放置一些复杂的业务逻辑代码 
  
  - 动画效果transitions：可以结合第三方 CSS 动画库，如 [Animate.css](https://daneden.github.io/animate.css/) 结合使用十分有用

- ### Vue生命周期 ###
  - beforeCreate：实例刚刚被创建，属性还没有
  - created：vue实例已经创建，有属性了
  - beforeCompile：编译之前，如编译{{msg}}里面的内容
  - compiled：编译之后 
  - ready：将结点插入到document文档中 （2.0后变为mounted）
  - beforeDestroy：在vue实例销毁之前 
  - destroyed： vue实例销毁之后 
  
  ![lifecycle.png](http://upload-images.jianshu.io/upload_images/5307186-eda1b28e54a4d48e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

- ### vue实例简单方法（var vm = new Vue(...)） ###
  - vm.$el：vue实例挂载的结点元素
  - vm.$data：就是data
  - vm.$mount：手动挂载vue 
  - vm.$options：获取自定义属性 
  - vm.destroy：销毁vue实例 
  - vm.$log：查看vue实例现在数据的状态 
  - vm.$watch：数据监听 

- ### webpack配置认识 ###
  - entry：配置入口js：main.js
  - output：配置打包后的信息
    - path：输出文件的路径(_dirname：文件当前所在目录地址)
    - filename：输出的文件名称：build.js
  - loaders：下载编译相关文件的loader，如：vue-loader、css-loader、vue-style-loader，vue-html-loader、vue-hot-reload-api等

- ### vue-cli 脚手架 ###
  安装：npm install vue-cli -g

- ### 父子组件通信 ###
  - 子组件获取父组件数据：props
  - 父组件获取子组件的数据：父组件可以在使用子组件的地方直接用 v-on 来监听子组件触发的事件
    - 使用 $on(eventName) 监听事件 
    - 使用 $emit(eventName) 触发事件
  
- ### 支持Vue的UI组件 ###
  - ElementUI（PC端） 
  - MintUI（移动端） 

- ### Vue自定义组件的写法 ###
  自定义组件可以使用Vue.use(componentName)方法引用，如编写loading.vue组件：
目录结构： 
       |- components/  
          |- loading/
            |- loading.vue
            |- index.js 
在loading.vue中按照一般组件的方式定义组件功能及样式模板，然后在index.js中导出组件:
  - index.js 
     ![1.png](http://upload-images.jianshu.io/upload_images/5307186-e4beabd257530fba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  - 最后在main.js中使用Vue.use 

- ### 监听路由变化 (使用vue-router) ###
         watch(){
              $route(to, from){
                  ...
              }
          } 
- ### axios发送http请求 ###
文档地址 : [https://github.com/mzabriskie/axios](https://github.com/mzabriskie/axios)