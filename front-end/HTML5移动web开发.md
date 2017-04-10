- ## Web app ， Native app 和 Hybrid app ##
   Hybrid是混合模式开发，介于webapp和native之间，各个手机终端能够公用一套开发代码，方便快速迭代更新。在手机上，利用UIWebview实现一个小浏览器，然后通过编写js桥，实现了web开发的介入。性能方面，hybrid模式与原生的native之前是有一定差距的，没有原生流畅。

- ## JavaScript的设计模式（待补充） ##
  - 单例模式
  - 实例化

- ## 响应式布局 ##
通过媒体查询实现 @media

- ## 涉及的技术 ##
  - 图片使用base64格式加载
  - 使用CSS3制作icon：体积小，但存在兼容性问题，比如border-radius制作圆角、transform作缩放、box-shadhow作阴影等等
  - H5技术
  - 移动端性能问题：
      - 减少对DOM元素的操作：减少从文档流里提取出dom元素进行操作
      - 尽可能缓存可以缓存的数据：app cach，manifest，localstorage， sessionstorage，web sql，indexedDB等等
      - 使用CSS3的transform来代替DOM的变换操作