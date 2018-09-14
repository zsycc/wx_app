Vuex
1.安装:(1)NPM:npm install vuex --save
       (2)Yarn:yarn add vuex
2.下载依赖文件:npm install
3.Vuex 依赖 Promise。如果你支持的浏览器并没有实现 Promise (比如 IE)，那么你可以使用一个 polyfill 的库
4.介绍:Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
5. 什么是“状态管理模式”:状态自管理应用包含以下几个部分：
                        state，驱动应用的数据源；
                        view，以声明方式将 state 映射到视图；
                        actions，响应在 view 上的用户输入导致的状态变化。
                        以下是一个表示“单向数据流”理念的极简示意:https://vuex.vuejs.org/flow.png
6.注意:(1)当我们的应用遇到多个组件共享状态时，单向数据流的简洁性很容易被破坏：
          多个视图依赖于同一状态。
          来自不同视图的行为需要变更同一状态。
       (2)虽然 Vuex 可以帮助我们管理共享状态，但也附带了更多的概念和框架。这需要对短期和长期效益进行权衡。如果您不打算开发大型单页应用，使用 Vuex 可能是繁琐冗余的。确实是如此——如果您的应用够简单，您最好不要使用 Vuex。
7.state:(1)单一状态树:用一个对象就包含了全部的应用层级状态。至此它便作为一个“唯一数据源 (SSOT)”而存在。这也意味着，每个应用将仅仅包含一个 store 实例。单一状态树让我们能够直接地定位任一特定的状态片段，在调试的过程中也能轻易地取得整个当前应用状态的快照。
(2)key值在哪里用了:App.vue
(3)怎么用的:computed 里面用的
(4)为什么要用computed (计算属性):data是有缓存的，一旦Vuex中值改变了，没法做到响应。而放在computed中，虽然也有缓存，但会自动监视依赖。
8.getters:(1)Vuex 允许我们在 store 中定义“getter”（可以认为是 store 的计算属性）。就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算
(2)通过方法访问:可以通过让 getter 返回一个函数，来实现给 getter 传参。在你对 store 里的数组进行查询时非常有用。
9.mutation:(1)更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数
(2)注意:mutation里只能执行同步操作。
10.action:(1)Action 类似于 mutation，不同在于：
              Action 提交的是 mutation，而不是直接变更状态。
              Action 可以包含任意异步操作。
(2)action并不修改数据 而是 提交给mutations
   API解释:Action 提交的是 mutation，而不是直接变更状态。
(3)context 与 接受一个与 store 实例具有相同方法和属性的 context 对象 == 当前store实例的(不完全等于) context.state 和当前的store里面的state一样
(4)分发 Action:action是通过store.dispatch 方法触发的,commit是触发mutations的,flag 是dispatch 传来的参数
(5)action 就不受约束！我们可以在 action 内部执行异步操作,也可以执行同步操作
(6)在组件中分发 Action:你在组件中使用 this.$store.dispatch('xxx') 分发 action，或者使用 mapActions 辅助函数将组件的 methods 映射为 store.dispatch 调用（需要先在根节点注入 store）
11.module:(1)作用:由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。
为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割
(2)模块的局部状态:对于模块内部的 mutation 和 getter，接收的第一个参数是模块的局部状态对象。
(3)Vuex 可以是一个单一状态树,也可以分割成更细的树 modules就是做这个的
12.严格模式:(1)开启严格模式，仅需在创建 store 的时候传入 strict: true
const store = new Vuex.Store({
  // ...
  strict: true
})
(2)开发环境与发布环境:不要在发布环境下启用严格模式！**严格模式会深度监测状态树来检测不合规的状态变更——请确保在发布环境下关闭严格模式，以避免性能损失。
