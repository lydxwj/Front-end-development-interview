# vue

## 1.v-if和v-show区别

- #### 手段：v-if是动态的向DOM树内添加或者删除DOM元素；v-show是通过设置DOM元素的display样式属性控制显隐；

- #### 编译过程：v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件；v-show只是简单的基于css切换；

- #### 编译条件：v-if是惰性的，如果初始条件为假，则什么也不做；只有在条件第一次变为真时才开始局部编译（编译被缓存？编译被缓存后，然后再切换的时候进行局部卸载); v-show是在任何条件下（首次条件是否为真）都被编译，然后被缓存，而且DOM元素保留；

- #### 性能消耗：v-if有更高的切换消耗；v-show有更高的初始渲染消耗；

- #### 使用场景：v-if适合运营条件不大可能改变；v-show适合频繁切换。

### 详情请参考:

http://www.cnblogs.com/wmhuang/p/5420344.html

## 2.vue组件之间传参

- #### 父与子组件传参1（父传子）

  - 父组件

    ```vue
    <template>
    	<div class='tmpl'>
    		<SubVue :tosubdata="tosubdata"></SubVue>
    		<sub-vue :tosubdata="tosubdata"></sub-vue>
    	</div>
    </template>
    <script>
    import SubVue from './sub.vue'
    	export default{
    		data(){
    			return {
    				tosubdata:'来自于parnet.vue组件的数据'
    			}
    		},
    		components:{  //负责注册所有要使用的子组件
    			SubVue  //注册sub.vue组件对象
    		}
    	}
    </script>
    <style>
    </style>
    ```

  - 子组件

    ```vue
    <template>
    	<div class='tmpl'>
    		<div class="subvue">{{msg}}
    			<div>{{tosubdata}} </div>
    		</div>
    	</div>
    </template>
    <script>
    	export default{
    		data(){
    			return {
    				msg:'这是sub.vue中的内容'
    			}
    		},
    		props:['tosubdata']
    	}
    </script>
    <style>
    </style>
    ```

- #### 父与子组件传参2（子传给父）

  - 父组件

    ```vue
    <template>
        <div class="tmpl">  
            购买数量：<sub-number class="subnumber" v-on:count="getcount"></sub-number>
        </div>
    </template>
    <style scoped>
    </style>
    <script>
    import SubNumber from '../subcomp/subnumber.vue';
        export default{
            data(){
                return{
                    goodscount:1, //商品的数量
                }
            },
            created(){         
            },
            methods:{
                //定义一个方法用来接收子组件传入过来的值
                getcount(obj){
                    this.goodscount = obj.count;
                }
            },
            components:{
                SubNumber
            }
        }
    </script>
    ```

  - 子组件

    ```vue
    <template>
        <div class="subtmpl">
            <div class="left" @click="substrict">-</div>
            <div class="middle">{{resObj.count}}</div>
            <div class="right" @click="add">+</div>
        </div>
    </template>
    <style scoped>
    </style>
    <script>
        export default{
            data(){
                return{
                    resObj:{type:ADD,goodsid:0,count:0}
                }
            }
            methods:{
               add(){
                    this.resObj.count++;
                    this.resObj.type=ADD;
                    this.notiflycount();
               },
                substrict(){
                    if(this.resObj.count <= 1){
                        this.resObj.count = 1;
                        return;
                    }
                    this.resObj.count--;
                    this.resObj.type=SUBSTRICT;
                    this.notiflycount();
                },
                notiflycount(){
                    let key = 'count';
                    this.$emit(key,this.resObj); //当执行了这个代码以后，就会自动触发父组件中的getcount()
                }
            }
        }
    </script>
    ```

- #### 组件传参3（没有父子关系）

  - 公共js

    ```jsx
    import Vue from 'vue';
    export  var vueobj = new Vue();
    ```

  - 传参组件

    ```vue
    <template>
        <div class="tmpl">
            <div class="sell">
                <mt-button type="danger" size="small" @click="toshopdata">加入购物车</mt-button>
            </div>
        </div>
    </template>
    <style scoped>
    </style>
    <script>
    //1. 注册commonvue.js
    import {vueobj} from '../../kits/commonvue.js';
        export default{
            data(){
                return{
                    goodscount:1, 
                }
            },
            methods:{            
                // 3.方法实现购物数据的通知
                toshopdata(){
                    vueobj.$emit('shopdata',this.goodscount);
                }
            }
        }
    </script>
    ```

  - 接收组件

    ```vue
    <template>
    	<nav  class="mui-bar mui-bar-tab">	
    		<span class="mui-icon mui-icon-home">
    			<span id="badge" class="mui-badge">0</span>
    		</span>
    			<span class="mui-tab-label">购物车</span>
    		</router-link>
    	</nav>
    </template>
    <script>
    	//1. 注册commonvue.js(用来接收goodsinfo.vue中通过vueobj.$emit()发送过来的数据 )
    	import {vueobj} from './kits/commonvue.js';
    	//2.注册接收事件
    	vueobj.$on('shopdata',function(data){
    		//由于vueobj和export default是不同的vue对象，所以在此处必须通过原生js来操作dom实现购物车数量的增加
    		let badge = document.getElementById('badge');
    		let count = badge.innerText - 0; 
    		count+=data;  
    		badge.innerText = count;
    	});
    </script>
    <style scoped>
    </style>
    ```

- #### vuex

#### 详情参考

https://blog.csdn.net/zhoulu001/article/details/79548350

## 3.vue路由

```
npm install vue-router --save
```

```jsx
import vueRouter form 'vue-router'
import Vue from 'vue'
Vue.use(vueRouter)
let router = new vueRouter({
	routes:[
		{name:'Login',path:'/Account/Login/:id/:name',component:Login},
		{name:'Register',path:'/Account/Register',component:Register},
		{name:'res',path:'/vueres',component:vueres},
	]
});
new Vue({
	el:'#app',
	router,
	render:c=>c(App)
});
```

## 4.vue生命周期

- #### `beforeCreate`

在实例初始化之后，数据观测(data observer) 和 event/watcher 事件配置之前被调用。

- #### `created`

实例已经创建完成之后被调用。在这一步，实例已完成以下的配置：数据观测(data observer)，属性和方法的运算， watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。

- #### `beforeMount`

在挂载开始之前被调用：相关的 render 函数首次被调用。

- #### `mounted`

el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。

- #### `beforeUpdate`

数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。

- #### `updated`

由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态，因为这可能会导致更新无限循环。

该钩子在服务器端渲染期间不被调用。

- #### `beforeDestroy`

实例销毁之前调用。在这一步，实例仍然完全可用。

- #### `destroyed`

Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 该钩子在服务器端渲染期间不被调用。

### 详情请参考:

https://segmentfault.com/a/1190000008010666

http://www.cnblogs.com/fly_dragon/p/6220273.html

## 5.vue监听对象的具体属性

```jsx
data() {
　　return {
　　　　bet: {
　　　　　　pokerState: 53,
　　　　　　pokerHistory: 'local'
　　　　}   
    }
},
computed: {
　　pokerHistory() {
　　　　return this.bet.pokerHistory
　　}
},
watch: {
　　pokerHistory(newValue, oldValue) {
　　　　console.log(newValue)
　　}
}
```

### 详情请参考:

http://www.jianshu.com/p/d01e145388fc

## 6.简介vuex

- #### Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

- #### 每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的**状态 (state)**。Vuex 和单纯的全局对象有以下两点不同：

  1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
  2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地**提交 (commit) mutation**。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用

- #### [安装](https://vuex.vuejs.org/zh-cn/installation.html) Vuex 之后，让我们来创建一个 store。创建过程直截了当——仅需要提供一个初始 state 对象和一些 mutations：

  ```vue
  // 如果在模块化构建系统中，请确保在开头调用了 Vue.use(Vuex)
  
  const store = new Vuex.Store({
    state: {
      count: 0
    },
    mutations: {
      increment (state) {
        state.count++
      }
    }
  })
  ```

- #### 现在，你可以通过 `store.state` 来获取状态对象，以及通过 `store.commit` 方法触发状态变更：

  ```vue
  store.commit('increment')
  console.log(store.state.count) // -> 1
  ```

- #### 再次强调，我们通过提交 mutation 的方式，而非直接改变 `store.state.count`，是因为我们想要更明确地追踪到状态的变化。

### 详情参考：

https://vuex.vuejs.org/zh-cn/

## 7.二级联动vue

http://blog.csdn.net/lllo3o/article/details/72955701

## 8.vue修饰符

### v-on

- `.stop` - 调用 `event.stopPropagation()`。
- `.prevent` - 调用 `event.preventDefault()`。
- `.capture` - 添加事件侦听器时使用 capture 模式。
- `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
- `.{keyCode | keyAlias}` - 只当事件是从特定键触发时才触发回调。
- `.native` - 监听组件根元素的原生事件。
- `.once` - 只触发一次回调。
- `.left` - (2.2.0) 只当点击鼠标左键时触发。
- `.right` - (2.2.0) 只当点击鼠标右键时触发。
- `.middle` - (2.2.0) 只当点击鼠标中键时触发。
- `.passive` - (2.3.0) 以 `{ passive: true }` 模式添加侦听器

### v-bind

- `.prop` - 被用于绑定 DOM 属性 (property)。([差别在哪里？](https://stackoverflow.com/questions/6003819/properties-and-attributes-in-html#answer-6004028))
- `.camel` - (2.1.0+) 将 kebab-case 特性名转换为 camelCase. (从 2.1.0 开始支持)
- `.sync` (2.3.0+) 语法糖，会扩展成一个更新父组件绑定值的 `v-on` 侦听器。

### v-model

- [`.lazy`](https://cn.vuejs.org/v2/guide/forms.html#lazy) - 取代 `input` 监听 `change` 事件
- [`.number`](https://cn.vuejs.org/v2/guide/forms.html#number) - 输入字符串转为有效的数字
- [`.trim`](https://cn.vuejs.org/v2/guide/forms.html#trim) - 输入首尾空格过滤

## 9.vue路由原理

- vue-rouetr在实现单页面前端路由时，提供了两种方式：**Hash模式**和**History模式**；根据mode参数来决定采用哪一种方式。

- Hash模式： 
      hash（#）是URL 的锚点，代表的是网页中的一个位置，单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页，也就是说 #是用来指导浏览器动作的，对服务器端完全无用，HTTP请求中也不会不包括#；同时每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；

- History模式： 

  HTML5 History API提供了一种功能，能让开发人员在不刷新整个页面的情况下修改站点的URL，就是利用 history.pushState API 来完成 URL 跳转而无须重新加载页面

- 通常情况下，我们会选择使用History模式，原因就是Hash模式下URL带着‘#’会显得不美观；但实际上，这样选择一不小心也会出问题；比如：

  但当用户直接在用户栏输入地址并带有参数时： 
  Hash模式：xxx.com/#/id=5 请求地址为 xxx.com,没有问题; 
  History模式: xxx.com/id=5 请求地址为 xxx.com/id=5，如果后端没有对应的路由处理，就会返回404错误；

- 为解决这一问题，vue-router提供的方法是：

  - 在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。 
  - 给个警告，因为这么做以后，你的服务器就不再返回 404 错误页面，因为对于所有路径都会返回 index.html 文件。为了避免这种情况，你应该在 Vue 应用里面覆盖所有的路由情况，然后在给出一个 404 页面。或者，如果你使用 Node.js 服务器，你可以用服务端路由匹配到来的 URL，并在没有匹配到路由的时候返回 404，以实现回退。

### 详情参考：

https://blog.csdn.net/github_39532240/article/details/79551130 

## 10.vue双向绑定原理

- 采用数据劫持结合发布者-订阅者模式的方式，通过`Object.defineProperty()`来劫持各个属性的`setter`，`getter`，在数据变动时发布消息给订阅者，触发相应的监听回调

- vue如何实现

  ![img](https://images2017.cnblogs.com/blog/1162184/201709/1162184-20170918135341618-553576179.png)

  - observer用来实现对每个vue中的data中定义的属性循环用Object.defineProperty()实现数据劫持，以便利用其中的setter和getter，然后通知订阅者，订阅者会触发它的update方法，对视图进行更新。
  - 我们介绍为什么要订阅者，在vue中v-model，v-name，{{}}等都可以对数据进行显示，也就是说假如一个属性都通过这三个指令了，那么每当这个属性改变的时候，相应的这个三个指令的html视图也必须改变，于是vue中就是每当有这样的可能用到双向绑定的指令，就在一个Dep中增加一个订阅者，其订阅者只是更新自己的指令对应的数据，也就是v-model='name'和{{name}}有两个对应的订阅者，各自管理自己的地方。每当属性的set方法触发，就循环更新Dep中的订阅者。

### 详情参考：

https://www.cnblogs.com/zhenfei-jiang/p/7542900.html

https://www.cnblogs.com/libin-1/p/6893712.html

## 11.vue页面缓存

- keep-alive是vue内置的一个组件，可以使被它包含的组件处于保留状态，或避免被重新渲染。

  ```
  <keep-alive>
  	<router-view v-if="$route.meta.keepAlive"></router-view>
  </keep-alive>
  ```

- `include` - 字符串或正则表达式。只有名称匹配的组件会被缓存。

  `exclude` - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。

  `max` - 数字。最多可以缓存多少组件实例。

- 路由

  ```
  {
  	path: '/',
  	meta: {keepAlive: true},
  	component: require('@/components/Home')
  },
  ```

### 详情参考：

https://blog.csdn.net/qq_38614249/article/details/79468609

## 12.vue和angular或react区别

- #### vue和angular

1. vue仅仅是mvvm中的view层，只是一个如jquery般的工具库，而不是框架，而angular而是mvvm框架。
2. vue的双向邦定是基于ES5 中的 getter/setter来实现的，而angular而是由自己实现一套模版编译规则，需要进行所谓的“脏”检查，vue则不需要。因此，vue在性能上更高效，但是代价是对于ie9以下的浏览器无法支持。
3. vue需要提供一个el对象进行实例化，后续的所有作用范围也是在el对象之下，而angular而是整个html页面。一个页面，可以有多个vue实例，而angular好像不是这么玩的。
4. vue真的很容易上手，学习成本相对低，不过可以参考的资料不是很丰富，官方文档比较简单，缺少全面的使用案例。高级的用法，需要自己去研究源码，至少目前是这样。

- #### vue/angular/react

  React 和 Vue 有许多相似之处，它们都有：
  1.使用 Virtual DOM
  2.提供了响应式（Reactive）和组件化（Composable）的视图组件。
  3.将注意力集中保持在核心库，伴随于此，有配套的路由和负责处理全局状态管理的库。 

  React 和 Vue 的区别：
  1.复杂性
  在 API 与设计两方面上 Vue.js 都比 Angular 1 简单得多，因此你可以快速地掌握它的全部特性并投入开发。
  2.灵活性和模块化
  Vue.js 是一个更加灵活开放的解决方案。它允许你以希望的方式组织应用程序，而不是在任何时候都必须遵循 Angular 1 制定的规则，这让 Vue 能适用于各种项目。我们知道把决定权交给你是非常必要的。 
  这也就是为什么我们提供 Webpack template，让你可以用几分钟，去选择是否启用高级特性，比如热模块加载、linting、CSS 提取等等。
  3.数据绑定
  Angular 1 使用双向绑定，Vue 在不同组件间强制使用单向数据流。这使应用中的数据流更加清晰易懂。
  4.指令与组件
  在 Vue 中指令和组件分得更清晰。指令只封装 DOM 操作，而组件代表一个自给自足的独立单元 —— 有自己的视图和数据逻辑。在 Angular 中两者有不少相混的地方。
  5.性能
  Vue 有更好的性能，并且非常非常容易优化，因为它不使用脏检查。

### 详情请参考:

http://blog.csdn.net/llm913114267/article/details/69068414

http://www.cnblogs.com/Zcqian/p/6843787.html

http://www.jb51.net/article/108388.htm

http://blog.csdn.net/qq_35844177/article/details/54915615