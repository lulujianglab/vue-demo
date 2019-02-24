# vue 基础

在讲 vue 之前，我们先提一下框架和库的区别

**库** — 类似于 jquery 这样的库，是操作 DOM 元素，发起 ajax 请求等，中间还会用到一些其他的库，用来做模板引擎

**框架** — 全方位功能齐全，请求获取数据，模板渲染，框架就是一个简易的DOM操作+发请求+模板引擎+路由功能

一个比较生活化的例子，比如KFC，库就是一个小套餐，框架就是全家桶

所以，框架就是更为全面的功能，库就是单一的层面

从代码层面上讲，一般使用库的代码，是调用某个函数，我们自己把控库的代码；而使用框架，是框架在帮我们运行我们编写好的代码

比如，框架运行时，一般会初始化自身的代码，然后执行你所编写的代码，最后释放一些资源，其中初始化代码和释放资源都是框架自身的功能

作为框架来讲，基本是大而全，而库就比较专一

从运行层面上讲，对于框架来说，是我们把代码给框架运行，库是我们调用库

## 插值表达式

* {{表达式}}

1. 对象(不要连接3个{{ {name:'jack'} }})
2. 字符串{{ 'xxx' }}
3. 判断后的布尔值 {{ true }}
4. 三元表达式 {{ true? '是正确':'错误' }}

* 可以用于页面中简单粗暴的调试

* 注意：必须在 data 这个函数中返回的对象中声明

## 什么是指令

* 比如在 angular 中以 ng-xxx 开头的就叫做指令
* 在 vue 中以 v-xxx 开头的就叫做指令
* 指令中封装了一些 DOM 行为，结合属性作为一个暗号，暗号有对应的值，根据不同的值，框架会进行相关 DOM 操作的绑定

## vue 中常见的 v- 指令演示

* v-text 元素的 innerText 属性必须是双标签
* v-html 元素的 innerHTML
* v-if 判断是否插入这个元素
* v-else-if
* v-else 移出和插入的问题，移出后是 `<!---->`
* v-show 隐藏元素，如果确定隐藏，会给元素的 style 加上 display:none 隐藏与否的问题

* v-text 只能用在双标签中
* v-text 其实就是给元素的 innerText 赋值
* v-html 其实就是给元素的 innerHTML 赋值
* v-if 如果值为 false，会留下一个 `<!---->` 作为标记，万一未来 v-if 的值是 true 了，就是这里插入元素，如果有 if 和 else 就不需要单独留坑了

## v-bind 使用

* 给元素的属性赋值

1. 可以给已经存在的属性赋值 input value
2. 也可以给自定义属性赋值 mydata

* 语法 在元素上 `v-bind:原属性名="变量||变量名"` 

* 简写形式 `:属性名=“变量名”`

## v-on的使用

* 处理自定义原生事件的，给按钮添加 click 并让使用变量的样式改变
* 在元素上 `v-on:原生事件名=“给变量进行操作||函数名”`
* 简写形式：`@原生事件名=“给变量进行操作”`

value 的值是根据 value 内部的变量，点击按钮，改变了 vue 内部的变量，vue 察觉到页面中使用的变量更改了，所以重新渲染了视图的更改部分

## 阶段总结：

* input 输入框中的 value 属性改变，显示就改变
* input 元素 .value = myValue = 'abc'
* vue 会实时监控 myValue 属性，当其改变，重新执行。将 vue 中的数据同步到页面，也是 v-bind 单向的功能
* 同时，当用户的输入值发生改变时，vue 就知道了让页面中凸显一个元素出来。页面的改变，影响 vue

  这就是双向数据绑定(流)，v-model="myValue"，当元素的 value 值改变以后，就会给 vue 中的属性赋值

v-bind 可以给任何属性赋值，是从 vue 到页面的单向数据流
v-model 只能给具备 value 属性的元素进行双向数据绑定(必须使用的是有 value 属性的元素)

## v-model

* 双向数据绑定

  1. 页面改变影响内存 ( js )
  2. 内存 ( js ) 改变影响页面

### v-bind 和 v-model 的区别

* `input v-model="name"`

  1. 双向数据绑定页面对于 input 的 value 改变，能影响内存中 name 变量
  2. 内存 js 改变 name 的值，会影响页面重新渲染最新值

* `input :value="name"`

  1. 单向数据绑定 内存改变影响页面改变

* v-model: 其的改变影响其他 v-bind: 其的改变不影响其他

* v-bind 就是对属性的简单赋值，当内存中值改变，还是会触发重新渲染

## v-for的使用

* 基本语法 `v-for="item in arr" `
* 对象的操作 `v-for="item in obj"`
* 如果是数组没有id
  `v-for="(item,index) in arr" :class="index"`
* 各中v-for的属性顺序
  数组 item,index
  对象 value,key,index

## 关于对象内的this

* vue 已经把以前 this 是 window 或者事件对象的问题搞定了
* methods 和 data 本身是在同一个对象中的，所以在该对象中可以通过 this 随意取
* this.xxx 取 data 中的值，this.xxxMethod 调 methods 中的方法

## 渲染组件-父使用子组件

1. 创建子组件(对象)

    `var Header = { template: '模板', data是一个函数，methods: 功能，components:子组件们}`

2. 在父组件中声明，根属性 `components: {组件名: 组件对象}`
3. 在父组件要用的地方使用 `<组件名></组件名>`
  注意：在不同框架中，有的不支持大写字母，用的时候
    * 组件名 MyHeader
    * 使用 my-header
4. 总结：有父、生子、声明、使用

## 父子组件传值(父传子)

1. 父用子的时候通过属性传递
2. 子要声明 props:['属性名']来接收
3. 收到就是自己的了，随便使用

    * 在 template 中直接用
    * 在 js 中 this 属性名用

4. 总结:父传，子声明，就是子的了
小补充：常量传递直接用，变量传递加冒号

## 总结父传子

* 父用子 先有子，声明子，使用子
* 父传子 父传子（属性），子声明（收），子直接用

## 注册全局组件

* 应用场景：多处使用的公共性功能组件，就可以注册成全局组件，减少冗余代码
* 全局API：`Vue.component('组件名'，组件对象)`

## 附加功能：过滤器&监视改动

1. filter

    * 将数据进行添油加醋的操作
    * 过滤器分为两种
      * 组件内的过滤器（组件内有效）
      * 全局过滤器（所有组件共享）
    * 先注册，后使用
    * 组件内 `filter:{过滤器名: 过滤器fn}`,最终 fn 内通过 return 产出最终的数据
    * 使用方式是 `{{原有数据|过滤器名}}`
    * 需求
      * 页面 input 框输入字符串，反字符串输出，按参数显示 label（中英文）
    * 过滤器 fn
      * 声明 `function(data,argv1,argv2...){}`

2. watch 监视单个

3. computed 监视多个

  * computed: {监视的业务名: function(){ return 显示的一些内容 }}
    * 使用 `计算属性的名称`

## slot（ 传递 DOM ）

* 内置的组件
* slot 就是子组件里给DOM留下的坑
* `<子组件>DOM</子组件>`
* slot 动态的 DOM，props 是动态的数据
 
实质上，slot 其实就是父组件传递给 DOM 结构

vue提供的内置组件 `<slot></slot>`

```js
<my-li>
  <button>111</button>
</my-li>
```

## 生命周期函数（钩子函数）

Vue 实例从创建到销毁的过程，就是生命周期

详细来说也就是从开始创建、初始化数据、编译模板、挂载 Dom、渲染→更新→渲染、卸载等一系列过程

* beforeCreate
* created
* beforeMount
* mounted
* beforeUpdate
* updated
* beforeDestroy
* destroyed

1. 在 beforeCreate 和 created 钩子函数之间的生命周期

    进行**初始化事件，进行数据的观测**，在 **created 的时候数据已经和 data 属性进行绑定**
    需要注意的是，**此时还是没有 el 选项**

2. created 钩子函数和 beforeMount 间的生命周期

    首先会判断对象是否有 **el 选项**。**如果有的话就继续向下编译，如果没有**el选项，**则停止编译**，**也就意味着停止了生命周期，直到在该 vue 实例上调用 vm.$mount(el)**

    如果 vue 实例对象中有 template 参数选项，则将其作为模板编译成 render 函数，如果没有 template 选项，则将外部 HTML 作为模板编译
    **template 中的模板优先级要高于 outer HTML 的优先级**

    render 函数选项 > template 选项 > outer HTML.

3. beforeMount 和 mounted 钩子函数间的生命周期

    给 vue 实例对象添加 **`$el` 成员**，并且替换掉挂在的 DOM 元素

    注意，**beforeMount 方法中 $el 还未被创建，这期间 VUE 先后生成两份模板，但是在 beforeMount 之前只是虚拟的，并未真实存在**

4. mounted

  `id="app"` 中的内容发生了变化

5. beforeUpdate 钩子函数和 updated 钩子函数间的生命周期

    当 vue 发现 data 中的数据发生了改变，会**触发对应组件的重新渲染**，先后**调用 beforeUpdate 和 updated** 钩子函数

    在 **beforeUpdate** 时,**可以监听到 data 的变化但是 view 层没有被重新渲染**，view 层的数据没有变化。等到 **updated** 的时候 **view 层才被重新渲染，数据更新**

    需要注意的是，这里运行 `console.log`，在 beforeUpdated 钩子函数执行的时候里面的 DOM 元素就已经发生了变化，是因为还有 `virtual DOM` 这一层,实际上，我们打印 `document.body.innerHTML`，view 层是没有被重新渲染的

6. beforeDestroy 和 destroyed 钩子函数间的生命周期
  
    beforeDestroy 钩子函数在实例销毁之前调用
    destroyed 钩子函数在 Vue 实例销毁后调用

    需要注意的是，**频繁的销毁和创建组件**会影响页面性能，如果需要频繁的操作，我们**可以使用 `<keep-alive></keep-alive>` 内置组件**来控制组件的激活和停用，用法也就是包裹住需要销毁的组件的就好了

    ```js
    <keep-alive>
        <test v-if="isExist"></test>
    </keep-alive>
    ```

    这个时候就用到了另一对**钩子函数 `activated` 和 `deactivated`** ,分别在**组件被激活和被停用时触发**

## 获取 DOM 元素

* 救命稻草，document.querySelector

  * 在 template 中标识元素 ref = "xxx"
  * 在要获取的时候，this.$refs.xxx 获取元素
      * 创建组件，装载 DOM，用户点击按钮

* ref 在 DOM 上获取的是原生 DOM 对象
* ref 在组件上获取的是组件对象

  * $el 是拿起 DOM
  * 这个对象就相当于我们平时玩的 this，也可以直接调用函数

## Vue.nextTick 对异步函数的结果进行操作

> 在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。

  需要了解的是 **Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按一定的策略进行 DOM 的更新**

  简单来说，Vue 在修改数据后，视图不会立刻更新，而是等同一事件循环中的所有数据变化完成之后，再统一进行视图更新

  ```js
  //改变数据
  vm.message = 'changed'

  //想要立即使用更新后的 DOM。这样不行，因为设置 message 后 DOM 还没有更新
  console.log(vm.$el.textContent) // 并不会得到 'changed'

  //这样可以，nextTick 里面的代码会在 DOM 更新后执行,有一定的延时
  Vue.nextTick(function(){
      console.log(vm.$el.textContent) //可以得到 'changed'
  })
  ```

需要注意的是，**在 created 和 mounted 阶段，如果需要操作渲染后的视图，要使用 nextTick 方法**
比如刷新页面时在 mouted 事件中触发 input 元素的插入，并给 input 元素获取焦点

```js
var App = {
  template: `<div>
    <input type="text" v-if="isShow" ref="input" />
  </div>`,

  data() {
    return {
      isShow: false
    }
  },
  mounted() {
    // 显示元素，并给与获取焦点
    this.isShow = true // 会触发 input 元素的插入,但这里并不会立马更新 DOM，最终代码更新完毕以后，vue才会根据实际的值，进行 DOM 的操作

    // 我们希望在 vue 真正渲染 DOM 到页面以后，才操作如下事件
    this.$nextTick(() => {
      this.$refs.input.focus()
    })
  },
}
```

> 注意 mounted 不会承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted

```js
mounted: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been rendered
  })
}
```

## 路由

### 路由原理

* 传统开发方式 url 改变后 立刻发起请求 响应整个页面 渲染整个页面 可能会出现白屏的问题
* SPA 锚点值改变后 不会发起请求 发起 ajax 请求 局部改变页面数据
  * 页面不跳转 用户体验更好

### SPA

* single page application ( 单页应用程序 )
* 前端路由
  * 锚点值监视
  * ajax 获取动态数据
  * 核心点是锚点值
* 前端框架 Vue / angular / react

### 命名路由

* 1. 给路由对象一个名称 `{ name: 'home', path: '/home', component: Home}`
* 2. 在 router-link 的 to 属性中描述这个规则

      * `<router-link :to="{name: 'home'}"></router-link>`
      * 通过名称找路由对象，获取其 path，生成自己的 href
       
* 大大降低维护成本，锚点值改变只用 main.js 中改变 path 属性即可

### 阶段总结

* vue-router 使用步骤：1.引入 2.安装插件 3.创建路由实例 4.配置路由规则 5.将路由对象关联 vue 6.留坑
* router-link to="/xxx" 命名路由
  1. 在路由规则对象中 加入 name 属性
  2. 在 router-link 中 :to="{name:"xxx"}"

### vue-router 中的对象

* $router 路由信息对象，只读对象
* $router 路由操作对象，只写对象

配置 `:to="{ name:'login',  query:{id:1}}` ，获取 `this.$route.query.id`，生成 `<a href="/detail?id=1">`

配置 `:to="{ name:'register', params:{name:'abc'}`，获取 `this.$route.params.id`，生成 `<a href="/detail/abc">`

### 嵌套路由

* 市面上所谓的用单页应用框架开发多页应用
  * 嵌套路由
* 案例
  * 进入我的主页显示；电影、歌曲
* 代码思想
  * router-view 的部分
    * router-view 第一层中，包含一个 router-view
  * 每一个坑挖好了，要对应单独的组件

### 知识点介绍 

* 路由 meta 元数据 => meta 是对于路由规则是否需要验证权限的配置
  * 路由对象中和 name 属性同级 { meta:{isChecked: true} }
* 路由钩子 => 权限控制的函数执行时期
  * 每次路由匹配后，渲染组件到 router-view 之前
  * `router.beforeEach(function(to,from,next){ })`

### 编程导航

* 跳到指定的锚点，并显示页面 `this.$router.push({name: 'xxx',query:{id:1},params:{name:'abc'} })`
* 配置规则 `{name:'xxx',path:'/xxx/:name'}`
* 根据历史记录，前进或后退

    * `this.$router.go(-1|1)`
    * 1代表进一步，-1是退一步

本质是锚点值的变化

## axios

可以看下 axios 的[中文文档](https://segmentfault.com/a/1190000008470355?utm_source=tuicool&utm_medium=referral)

> 浏览器端发起 XMLHttpRequests 请求
> node 端发起 http 请求
> 支持 Promise API
> 拦截请求和返回
> 转化请求和返回（数据）
> 取消请求
> 自动转化 json 数据
> 客户端支持抵御 XSRF（跨站请求伪造）

不像 jquery 那样嵌套，而是用 promise 
只做 ajax 请求 不做其他的 DOM 之类的请求