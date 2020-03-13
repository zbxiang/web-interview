# web-interview
前端面试题总结

# HTML中行内元素已块级元素的区别
1、行内元素与块级元素可以相互转换，通过修改display属性值来切换元素和行内元素，行内元素display:inline，块级元素display:block;
2、行内元素和其他行内元素都会在一条水平线上排列，都是在同一行的；块级元素却总是会在新的一行开始排列，各个块级元素独占一行，垂直向下排列，若想使其水平方向排列，可使用左右浮动，让其水平方向排列。
3、行内元素不可以设置宽度，宽度高度随文本内容的变化而变化，但是可以设置行高，同时在设置外边距margin上下无效，左右有效，内填充padding上下无效，左右有效，块级元素可以设置宽度，并且宽度高度以及外边距，内填充都可随意控制。
4、块级元素可以包含行内元素和块级元素，还可以容纳内联元素和其他元素，行内元素不能包含块级元素，只能容纳文本或者其他行内元素。

# 什么是闭包
简单来说，闭包是指可以访问另一个函数作用域变量的函数，一般是定义在外层函数中的内层函数。
函数作用域
内存回收机制
作用域继承

#  为什么需要闭包呢
局部变量无法共享和长久的保存，而全局变量可能造成变量污染，所以我们希望有一种机制既可以长久的保存变量又不会造成全局污染。


# 闭包的作用是什么？
保护
保存

# 闭包的运用场景
设计私有的方法和变量

# 特点
即想反复使用，又想避免全局污染

# 闭包的注意事项
通常，函数的作用域及其所有变量都会在函数执行结束后被销毁，但是，在创建了一个闭包以后，这个函数的作用域就会一直保存到闭包不存在为止。

# 闭包的缺陷
闭包的缺点就是常驻内存会增大内存使用量，并且使用不当很容易造成内存泄露
如果不是因为某些特殊任务而需要闭包，在没有必要的情况下，在其他函数中创建函数是不明智的，因为闭包对脚本性能具有负面影响，包含处理速度和内存消耗。

# cookie、localStorage和sessionStorage三者之间的区别
三者的异同

生命周期:
cookie：可设置失效时间，没有设置的话，默认是关闭浏览器失效
localStorage: 除非被手动清除，否则将会永久保存
sessionStorage: 仅在当前网页会话下有效，关闭页面或浏览器就会被清除。

存放数据大小:
cookie: 4kb左右
localStorage和sessionStorage：可以保存5MB的信息

http请求：
cookie: 每次都会携带在HTTP中，如果使用cookie保存过多数据会带来性能问题
localStorage和sessionStorage: 仅在客户端（即浏览器）中保存，不参与和服务器的通信

运用场景:
从安全性来说，因为每次http请求都会携带cookie信息，这样无形中浪费了宽带，所以cookie应该尽可能少的使用，另外cookie还需要指定作用域，不可以跨域调用，限制比较多，但是用来识别用户登录来说，cookie还是比storage更好用的。其他情况下，可以使用storage,就用storage.

storage在存储数据的大小上面秒杀了cookie，因为更大总是更好的。

localStorage和sessionStorage唯一的差别一个是永久保存在浏览器里面，一个是关闭网页就清除了信息。localStorage可以用来夸页面传递参数, sessionStorage用来保存一些临时的数据，防止用户刷新页面之后丢失了一些参数。

浏览器支持情况
localStorage和sessionStorage是html5才应用的新特性，可能有些浏览器并不支持，这里要注意。


# 前端性能优化的常用手段
浏览器渲染页面的过程

减少HTTP请求
CSS/JS 合并打包
小图标等用iconfont代替：作为单个DOM节点使用，可以设置大小、颜色等，非常便利。
使用base64格式的图片：有些小图片，可能色彩比较复杂，这个时候再用iconfont就有点不合适了，此时可以将其转化为base64格式（不能缓存），直接嵌在src中，比如webpack的url-loader设置limit参数即可

减少静态资源的体积
压缩静态资源：合并打包的js、css文件体积一般会比较大，一些图片也会比较大，这个时候必须要压缩处理。前后端分离项目，不论是gulp还是webpack，都有相应的工具包。针对个别图片，有时候也可以单独拿出来处理，我个人经常使用这个网站 tinypng.com/ 在线压缩

编写高效率的CSS：涉及到代码层面的优化比较多也比较细，不同水平的技术人员写出来的肯定不一样，这里不做进一步的分析。但是为什么要把CSS拿出来说一说呢？因为现在项目里面基本上都在使用CSS预处理器，Less、SaaS、Stylus等等，这导致了某些初级前端的滥用：嵌套5、6层，甚者能达到7、8层，吓死个人！嵌套这么深，影响浏览器查找选择器的速度不说，这也一定程度上产出了很多冗余的字节，这个要改、要提醒，一般建议嵌套3层即可。

服务端开启gzip压缩：大招，最近刚知晓，真是太牛逼了，一般的css、js文件能压缩60、70%，当然，这个比率可以设定的。前后端分离，如果前端部署用node、express作服务器的话，使用中间件compression即可开启gzip压缩

使用缓存
设置Http Header里面缓存相关的字段，做进一步的优化。
express里面也有对静态资源相关的设置，只不过平时没怎么注意：
可以设置etag、maxAge等，进一步会有200缓存和304缓存的区别：
200 OK (from cache) 是浏览器没有跟服务器确认，直接用了浏览器缓存；而 304 Not Modified 是浏览器和服务器多确认了一次缓存的有效性，然后再使用的缓存。

代码分割
分离第三方库代码
动态导入
提取复用的业务代码
分离非首页使用且复用程度小的第三方库

脚本加载的优化
要解决上面说到的脚本加载问题，通常有三种解决方案：将脚本放在HTML末尾、动态加载脚本以及异步加载脚本。最常用的应该就是将所有脚本放置在HTML文档的末尾了。这应该是每个前端刚入门时，被教的最多的。对于这个方法，这里就不多做介绍，直接上重头戏

动态加载
所谓动态加载脚本就是利用javascript代码来加载脚本，通常是手工创建script元素，然后等到HTML文档解析完毕后插入到文档中去。这样就可以很好地控制脚本加载的时机，从而避免阻塞问题。

function loadJS(src) {
  const script = document.createElement('script');
  script.src = src;
  document.getElementsByTagName('head')[0].appendChild(script);
}
loadJS('http://example.com/scq000.js');


异步加载
我们都知道，在计算机程序中同步的模式会产生阻塞问题。所以为了解决同步解析脚本会阻塞浏览器渲染的问题，采用异步加载脚本就成为了一种好的选择。利用脚本的async和defer属性就可以实现这种需求：
<script type="text/javascript" src="./a.js" async></script>
<script type="text/javascript" src="./b.js" defer></script>

虽然利用了这两个属性的script标签都可以实现异步加载，同时不阻塞脚本解析。但是使用async属性的脚本执行顺序是不能得到保证的。而使用defer属性的脚本执行顺序可以得到保证。另一方面，defer属性是在html文档解析完成后，DOMContentLoaded事件之前就会执行js。async一旦加载完js后就会马上执行，最迟不超过window.onload事件。所以，如果脚本没有操作DOM等元素，或者与DOM时候加载完成无关，直接使用async脚本就好。如果需要DOM，就只能使用defer了。

懒加载(lazyload)
懒加载是一种按需加载的方式，也通常被称为延迟加载。主要思想是通过延迟相关资源的加载，从而提高页面的加载和响应速度。在这里主要介绍两种实现懒加载的技术：虚拟代理技术以及惰性初始化技术。

虚拟代理加载

所谓虚拟代理加载，即为真正加载的对象事先提供一个代理或者说占位符。最常见的场景是在图片的懒加载中，先用一种loading的图片占位，然后再用异步的方式加载图片。等真正图片加载完成后就填充进图片节点中去。
// 页面中的图片url事先先存在其data-src属性上
const lazyLoadImg = function() {
  const images = document.getElementsByTagName('img');
  for(let i = 0; i < images.length; i++) {
      if(images[i].getAttribute('data-src')) {
          images[i].setAttribute('src', images[i].getAttribute('data-src'));
          images[i].onload = () => images[i].removeAttribute('data-src');
      }
  }
}

DNS Prefetch 预解析
还有一个可以优化网页速度的方式是利用dns的预解析技术。同preload类似，DNS Prefetch在网络层面上优化了资源加载的速度。我们知道，针对DNS的前端优化，主要分为减少DNS的请求次数，还有就是进行DNS预先获取。DNS prefetch就是为了实现这后者。其用法也很简单，只要在link标签上加上对应的属性就行了。

尽量减少 HTTP 请求个数——须权衡
使用 CDN（内容分发网络）
为文件头指定 Expires 或 Cache-Control ，使内容具有缓存性。
避免空的 src 和 href
使用 gzip 压缩内容
把 CSS 放到顶部
把 JS 放到底部
避免使用 CSS 表达式
将 CSS 和 JS 放到外部文件中
减少 DNS 查找次数
精简 CSS 和 JS
避免跳转
剔除重复的 JS 和 CSS
配置 ETags
使 AJAX 可缓存
尽早刷新输出缓冲
使用 GET 来完成 AJAX 请求
延迟加载
预加载
减少 DOM 元素个数
根据域名划分页面内容
尽量减少 iframe 的个数
避免 404
减少 Cookie 的大小
使用无 cookie 的域
减少 DOM 访问
开发智能事件处理程序
用  代替 @import
避免使用滤镜
优化图像
优化 CSS Spirite
不要在 HTML 中缩放图像——须权衡
favicon.ico要小而且可缓存
保持单个内容小于25K
打包组件成复合文本

# 一个请求从发出到返回结果经历了什么？
用户首先在浏览器中输入一个url，浏览器中的核心代码会将url进行拆分解析。浏览器会将domain发送到dns服务器，dns服务器会根据domain查询对应的ip地址，同时将ip地址返回给浏览器，浏览器在持有ip地址之后，就会知道这个请求要发送的地址，就跟随协议，将ip地址打在协议中，并且请求相关的参数都携带，发送到我们的网络中，经过局域网、交换机、路由器、主干网络，之后请求会到达我们的服务端，服务端是MVC架构，请求会首先进入到controller中，在controller中进行相关逻辑的分发，调用model层，model是与数据进行交互的，在数据进行交互中，去拿数据库的数据，最后将我们渲染好的数据通过view层分发到网络中，http请求的response就从服务端又回到了浏览器，浏览器就开始render。

# 潜在的性能优化点：
1、dns缓存
2、减少http请求
3、减小http请求的大小
4、网络请求的时候走最近的网络请求
5、浏览器端缓存

# 一个网站在浏览器端是如何进行渲染的？
请求返回一段HTML文档，这一段HTML文档会被浏览器中的HTML parse 这一个解析器进行解析，通过词法分析的过程将tag分析为token，依次从html文档中从上到下去解析token，因为他是用next token的方式不断的从上到下进行解析的，在词法分析的过程中是可以相应的解析出link script这样的标签，这样的标签里面所对应的web资源会进一步的由浏览器向网络发起请求。请求回来的JavaScript web资源会交给浏览器中的v8 JavaScript执行引擎去执行。css相关的资源请求回来之后会由浏览器生成相应的CSSOM树。页面渲染的前提是DOM树和CSSOM树都有了之后，去生成Render tree，进一步进行一个布局，从而进行绘制。

# 重绘与回流
问题
浏览器重绘与回流机制
什么是重绘
什么是回流
哪些操作能够出噶重绘和回流？

浏览器对URL进行DNS解析
浏览器与服务器进行TCP连接
浏览器发出HTTP请求
服务器返回HTTP响应
浏览器进行页面渲染

# 为何在v-for中用key
必须用key, 且不能是index和random
diff算法中通过tag和key来判断，是否是sameNode
减少渲染次数，提升渲染性能

# 描述Vue组件生命周期 (父子组件)
单组件生命周期图
父子组件生命周期关系

# Vue组件如何通讯(常见)
父子组件props和this.$emit
自定义事件event.$no event.$off event.$emit
vuex

# 描述组件渲染和更新的过程
(Component Render Function) render (Virtual DOM Tree)
(Touch) (Data getter setter) (Collect as Dependency) (Notify) 
(Watcher) (Trigger re-render)

# 双向数据绑定 v-model的实现原理
input 元素的 value = this.name
绑定 input 事件 this.name = $event.target.value
data 更新触发 re-render

# 对 MVVM 的理解

# computed 有何特点
缓存 data不变不会重新计算
提高性能

# 为何组件 data 必须是一个函数

# ajax 请求应该放在哪个生命周期
mounted
JS 是单线程的 ajax异步获取数据
放在 mounted 之前没有用，只会让逻辑更加混乱

# 如何将组件所有props传递给子组件
$props
<User v-bind="$props">
细节知识点 优先级不高

# 如何自己实现 v-model
<template>
  <input 
    type="text"
    :value="text"
    @input="$emit('change', $event.target.value)">

  <!--
    注意
    第一，上面使用:value 而没用 v-modal
    第二, 上面的 change 和 model.event 对应起来即可，名字自己改
  -->
</template>

<script>
export default {
  model: {
    prop: 'text', // 对应到 props text
    event: 'change'
  },
  props: {
    text: String
  }
}
</script>

# 多个组件有相同的逻辑，如何抽离
mixin
以及mixin的一些缺点

# 何时要使用异步组件
加载大组件
路由异步加载

# 何时需要使用keep-alive
缓存组件，不需要重复渲染
如多个静态tab页的切换
优化性能

# 何时需要使用 beforeDestory
解绑自定义事件 event.$off
清除定时器
解绑自定义的DOM事件，如 window scroll 等

# 什么是作用域插槽
<template>
  <a :href="url">
    <slot :website="website">
      {{website.subTitle}} <!-- 默认值显示 subTitle -->
    </slot>
  </a>
</template>

<script>
export default {
  props: ['url'],
  data() {
    return {
      website: {
        url: 'http://wangEditor.com/',
        title: 'wangEditor',
        subTitle: '轻量级富文本编辑器'
      }
    }
  }
}
</script>

<ScopedSlotDemo :url="website.url">
  <template v-slot="slotProps">
    {{ /* slotProps 名字可自定义 */ }}
    {{slotProps.website.title}}
  </template>
</ScopedSlotDemo>

# Vuex 中 actions 和 mutation 有何区别
action 中处理异步，mutation 不可以
mutation 做原子操作
action 可以整合多个 mutation

# Vue-router 常用的路由模式
hash 默认
H5 history (需要服务端支持)

# 如何配置 Vue-router 异步加载
export default new VueRouter({
  routes: [
    {
      path: '/',
      component: () => import(
        /* webpackChunkName: "navigator" */
        './../components/Navigator'
      )
    },
    {
      path: '/feedback',
      component: () => import(
        /* webpackChunkName: "feedback" */
        './../components/FeedBack'
      )
    }
  ]
})

# 请用 vnode 描述一个 DOM 结构
<div id="div1" class="container">
  <p>vdom</p>
  <ul style="font-size: 20px">
    <li>a</li>
  </ul>
</div>

{
  tag: 'div',
  props: {
    className: 'container',
    id: 'div1'
  }
  children: [
    {
      tag: 'p',
      children: 'vdom'
    },
    {
      tag: 'ul',
      props: { style: 'font-size: 20px' },
      children: [
        {
          tag: 'li',
          children: 'a'
        }
      ]
    }
  ]
}

# 监听 data 变化的核心 API 是什么
Object.defineProperty
以及深度监听、监听数组
有何缺点

# Vue 如何监听数组变化
Object.defineProperty 不能监听数组变化
重新定义原型，重写 push pop 等方法，实现监听
Proxy 可以原生支持监听数组变化

# 请描述响应式原理
监听 data 变化
组件渲染和更新的流程

# diff 算法的时间复杂度
O(n)
在O(n^3)基础上做了一些调整

# 简述 diff 算法过程
patch(elem, vnode) 和 patch(vnode, newVnode)
patchVnode 和 addVnodes 和 removeVnodes
updateChildren (key的重要性)

# Vue 为何是异步渲染，$nextTick何用
异步渲染（以及合并 data 修改）,以提高渲染性能
$nextTick 在 DOM 更新完之后，触发回调

# Vue 常见性能优化方式
合理使用 v-show 和 v-if
合理使用 computed
v-for时加key, 以及避免和 v-if 同时使用
自定义事件、DOM事件及时销毁
合理使用异步组件
合理使用keep-alive
data 层级不要太深