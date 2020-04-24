<!--
 * @Descripttion: 
 * @version: 
 * @Author: lujj
 * @Date: 2020-03-05 14:42:02
 * @LastEditors: sueRimn
 * @LastEditTime: 2020-04-24 16:24:31
 -->
# vue-music

该项目已经打包部署
url:http://47.101.46.148:9000

## 生命周函数
每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会。

1. beforeCreate() 第一个生命周期函数：
表示实例被完全创建之前运行出来。
2. created() 第二个生命周期函数 ：
data   and  methods 已经初始化好了。
3. beforeMount() 第三个生命周期函数：
模板已经再内存中编译完成，但是尚未把模板渲染到页面中去。
4. mounted() 第四个周期函数：
内存中的模板 已经真实挂在到了页面中，dom上树了，可以看到渲染好的页面了，当执行完这个，实例已经完全创建好了。 
5. beforeUpdate()第五个周期函数 ：
这俩事件会根据data数据的改变，有选择性的出发0-n次。
6. updated()第六个周期函数 ：
执行的手页面和data的数据已经保持同步了 都是最新的。
7. beforeDestroy() 第七个周期函数 :
当执行这里的时候就已经从运行阶段进入到了销毁阶段了。
8. destroyed() 第八个周期函数
执行到这里的时候组件已经被完全销毁，组件中所有的数据方法指令过滤器 都已经不可用了。


## vue-router
路由重定向，嵌套路由和动态路由。
默认页面用路由重定向。
歌手详情页面可以用嵌套路由。
歌手页面跳转到歌手详情页面可以通过singer.id来动态跳转。

## jsonp跨域和代理服务器

在获取推荐页面和歌手的数据是用jsonp就能解决，但是当我们获取歌手详情页面的歌曲数据时，用jsonp就解决不了了，
因为这个接口是一个 xhr 的 ajax 请求，所以我们不能直接请求这个接口，需要做一层代理。
这里我代理了一个 get 请求，我们本地实现了 /api/getDiscList这个 get 接口，并且接受的是 json 格式的数据，然后转发给 QQ 官网接口的时候，我们添加了 headers，伪造了 referer 和 host，目的就是为了满足 QQ 官网接口的请求格式。详细代码可以看vue.config.js。


## Vuex状态管理

每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state)。Vuex 和单纯的全局对象有以下两点不同：
1.  Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
2.  不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。
         我们也可以用vuex来实现同样的功能，来实现vuex与vue的类比。其实原理都是一样的，在vuex中有四个部分：state 、 mutations 、 actions 、getters类比，可以先假设没有 actions的情况下：
他们的对应关系是这样的：
（1）更改数据 mutations->methods（2）获取数据 getters -> computed（3）数据       state->data
视图通过点击事件，触发mutations中方法，可以更改state中的数据，一旦state数据发生更改，getters把数据反映到视图。
action可以理解是为了处理异步，而单纯多加的一层。要是没有设计上可以没有这一步。
在vue例子中，我们触发的click事件，就能触发methods中的方法，这是vue设计好的。而在vuex中则不行了，一定要有个东西来触发才行，就相当于自定义事件on，emit。vuex中的action，mulation通过on自定义的方法，相应的需要emit来触发。
他们的关系是这样的： 通过dispatch可以触发actions中的方法，actions中的commit可以触发mulations中的方法。
