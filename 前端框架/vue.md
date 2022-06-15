###https://zhuanlan.zhihu.com/p/92407628
###https://www.cnblogs.com/wenshaochang123/p/14888494.html

###1. Vue的优点

    1. 轻量级框架：只关注视图层，是一个构建数据的视图集合，大小只有几十kb；
    
    2. 简单易学：国人开发，中文文档，不存在语言障碍，易于理解和学习；
    
    3. 双向数据绑定：保留了angular的特点，在数据操作方面更为简单；
    
    4. 组件化：保留了react的优点，实现了htlm的封装和重用，在构建单页面应用方面有着独特的优势；
    
    5. 视图、数据、结构分离：使数据的更改更为简单，不需要进行逻辑代码的修改，只需要操作数据就能完成相关操作；
    
    6. 虚拟DOM，dom操作是非常耗费性能的，不再使用原声的dom操作节点，极大解放了dom操作，但是还是会具体操作dom，只是换了一种方式；
    
    7. 运行速度更快，相比较于react而言，同样是操作虚拟dom，就性能而言，vue存在很大的优势；
    
###2. 父组件向子组件传递数据：
    通过props
###3. 子组件调用父组件方法：
    1. 在父组件中通过v-on指令，对子组件设置监听某个事件；然后在子组件内部通过this.$emit('eventname')触发这个事件；
    2. 在父组件中通过v-bind把方法作为属性传入到子组件中；然后在子组件内部通过this.$props.event()调用父组件的方法；
    3. 在子组件中直接通过this.$parent.event()调用父组件的方法；
###4. v-show和v-if指令：
    共同点：都能够控制元素的显示与隐藏；
    不同点：v-show的本质是通过控制元素的CSS属性display，而v-if是通过动态地向DOM树中添加或删除DOM元素，
    总结：v-if因此需要不停地销毁和创建DOM，更加消耗性能，如果需要频繁切换某个节点，优先使用v-show；
    
    拓展补充：display: none、visibility: hidden、opacity: 0的区别
        1. 是否占据DOM位置：
            display：none隐藏之后不会占据空间，会导致重排和重绘，
            visibili：hidden和opacity：0依旧会占据空间，只会导致重绘；
        2. 子元素是否继承：
            display：none： 不会被继承，但是由于父元素已经不在DOM树中了，因此就算不会继承该属性，子元素也不会显示出来；
            visibility：hidden：会被继承，可以通过设置子元素visibility: visible来显示子元素；
            opacity: 0: 会被子元素继承，但是不能设置子元素opacity：0来重新显示子元素；
        3. 事件绑定： 
            display: none： 元素已经不占据空间，因此无法触发绑定事件；
            visibility: hidden： 不会触发绑定的事件；
            opacitiy：0： 依然会触发绑定事件；
        简要记法：
            display：none不占据空间，但是DOM节点依旧保留在DOM树中；
            visibility：hidden相相当于将元素整个替换成了空白的容器，也没有事件绑定；
            opacity：0相当于将元素的颜色设置为了透明，其余事件绑定都还存在；
###6. 如何让css只在当前组件中起作用？
    在组件的style标签中加上scoped
###7. keep-alive组件
    概念：keep-alive是Vue的内置组件，可以实现组件缓存，当组件切换时不会对当前组件进行卸载；
        和transition相似，keep-alive 是一个抽象组件：它自身不会渲染成一个 DOM 元素，也不会出现在父组件链中。
        常用的两个属性include/exclude，允许有条件的进行缓存（通过组件的name判断）；

    作用：在组件切换过程中将状态保留在内存中，防止重复渲染DOM，减少加载时间及性能消耗，提高用户体验性。

    原理：在created函数调用时将需要缓存的VNode节点保存在 this.cache 中，在 render（页面渲染）时；
        如果VNode的name符合缓存条件（可以用 include 以及 exclude 控制），则会从this.cache中取出之前缓存的VNode实例进行渲染；
        （VNode：虚拟DOM，其实就是一个JS对象）；

    两个生命周期activated/deactivated，用来得知当前组件是否处于活跃状态。

    keep-alive运用了LRU算法，选择最近最久未使用的组件予以淘汰：
        1. 将新数据从尾部插入到this.keys中，
        2. 每当缓存命中（即缓存数据被访问），则将数据移动到this.keys的尾部
        3. 当this.keys满的时候，将头部的数据丢弃

###8. 如何获取dom？
    通过模版引用，首先给元素设置ref属性(<div ref='domName' />)，然后通过 this.$refs.domName 获取DOM；
###9. Vue当中的指令和用法：
    1. v-text: 更新元素的textContent；
    2. v-html: 更新元素的innerHTML，内容将会按照普通HTML插入（不会作为Vue模版进行编译）；
    3. v-show: 切换元素的CSS display属性；
    4. v-if/v-else-if/v-else: 控制元素的展示或者隐藏，原理是动态地操作DOM（添加或者删除）；
    7. v-for: 基于源数据多次渲染元素或模板块；
    8. v-on: 用于绑定事件监听器（原生DOM事件和自定义事件），并且可以指定修饰符、以及绑定多个监听器；
    9. v-bind: 动态绑定元素的属性、或者组件的prop；
    10. v-model: 在表单控件或组件上创建双向绑定；
    11. v-slot: 提供具名插槽或需要接收 prop 的插槽；
    12. v-pre: 跳过这个元素以其子元素的编译过程，元素的内容将会被直接渲染出来，跳过大量没有指令的节点会加快编译；
    13. v-cloak: 这个指令会保持在元素上，直到关联组件实例结束编译，一般用于防止页面加载时出现 vuejs 的变量名(配合css选择器)；
    14. v-memo: 记住一个模板的子树。元素和组件上都可以使用，如果数组中的每个值都和上次渲染的时候相同，则整个该子树的更新会被跳过。
###10. v-for为什么要使用key
    key可以来为每一个节点做一个唯一标识，这样Diff算法就可以正确识别这个DOM，作用是为了更高效地更新虚拟DOM；
    
    如果不使用key，Vue会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法；
    key是为Vue中Vnode的唯一标识，通过这个key，我们的diff操作可以更加准确，更加快速；
        1. 更准确：因为带key就不是就地复用了，在sameNode函数a.key === b.key对比中就可以避免就地复用的情况，所以更加准确； 
        2. 更快速：利用key的唯一性生成map对象来获取对应节点，比遍历方式快；
###11. v-model的使用
    v-model通常用于表单数据的双向绑定，实际上它的本质是一个语法糖，背后就做了两个操作：
    1. v-bind绑定一个value属性；
    2. v-on绑定一个input事件；
###11. 简述computed、watchEffect和watch的使用场景：
    computed：
        computed是计算属性，依赖于其他属性来计算值，并且computed的值具有缓存，只有当计算值变化时才会返回内容；
        当多条数据影响一条数据的时候使用；
        PS: computed可以设置getter和setter；
    watch：
        可以侦听特定的数据源，当数据源发生改变时，在单独的回调函数中执行副作用；
        当一条数据影响多条数据时使用；
    watchEffect：
        根据响应式状态自动应用和重新应用副作用，无需指定依赖项；
###12 watch和watchEffect的区别：
    watch是需要传入侦听的数据源，而watchEffect是自动收集数据源作为依赖。
    watch可以访问侦听状态变化前后的值，而wat123456Effect没有，watchEffect获取的改变后的值。
    watch是属性改变的时候执行，而watchEffect是默认至少会执行一次。
###11. v-on可以监听多个事件吗
    可以，例如：<input v-on="{click: onClick, focus: onFocus}" />
###11. $nextTick的使用；
    作用：将回调推迟到下一个DOM更新周期之后执行。在更改了一些数据以等待 DOM 更新后立即使用它，可获取更新后的DOM。
    原理：Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中，原因是在created()钩子函数执行的时候DOM并未挂载。

    主要思路就是采用微任务优先的方式调用异步方法去执行nextTick包装的方法；

###11. Vue中的data为什么是一个函数
    组件中的data以函数返回值的形式定义，因此每次复用组件的时候，都会初始化一份新的data；
    相当于每个组件实例都有自己私有的数据空间，每个组件实例都只负责维护各自的数据，不会造成混乱；
    如果将写成对象形式，那么所有的组件实例将会共用一个data；
###11. 渐进式框架的理解
    主张最少，可以更具不同需求选择不同的层级；    
    渐进式框架就是一开始不需要你完全掌握它的全部功能特性，可以后续逐步增加功能，专注需求，可以选择性忽略一些不必要的功能；
    Vue.js只提供了vue-cli生态系统中最核心的组件系统和双向数据绑定；
    
    使用Angular，必须接受一下东西：
    1. 必须使用它的模块机制；
    2. 必须使用它的依赖注入；
    3. 必须使用它的特殊形式定义组件
    
    使用React，你必须理解：
    1. 函数式编程的理念
    2. 需要知道React副作用
    3. 需要知道什么是纯函数
    4. 如何隔离、避免副作用

###11. 发布订阅模式
    发布订阅模式包含3个元素：发布者，消息中心，订阅者；
    当某个任务完成后，发布者可以向消息中心发送一个信号，而订阅者可以向消息中心订阅这个信号；
    这样每次发布者发布新消息时，消息中心都会对订阅者发送一个通知；

###11. Vue2中双向数据绑定是如何实现的
    vue双向数据绑定指的是数据和视图同步，是通过数据劫持，结合发布订阅模式的方式来实现的（数据劫持 + 观察者模式）；

    基本概念：
        监听器Observer：用来劫持并监听所有属性，如果有变动的，就通知订阅者
        订阅者Watcher：每个Watcher都绑定了一个更新函数，Watcher可以接收到属性的变化通知并执行相应的函数，从而更新视图
        消息订阅器Dep：因为订阅者Watcher有多个，所以需要一个消息订阅器Dep来专门收集这些订阅者，在监听器Observe和订阅者Watcher之间进行统一管理；
        解析器Compile：可以扫描和解析每个节点的相关指令，若节点存在指令，则Compiler会初始化这类节点的模板数据，以及初始化相应的订阅者。

    原理：
        首先在vue初始化的时候，监听器Ovserver会对data选项返回的数据进行了劫持监听（通过Object.defineProperty）；
        若属性发生变化，就会立即通知消息订阅器Dep，然后再由消息订阅器Dep去通知订阅者触发更新；
        还需要有一个指令解析器会对模版的每个节点元素进行扫描解析，将相关的指令（如 v-model，v-on …）对应初始化成一个订阅者Watcher，并替换模板数据或者绑定相应函数；
        当订阅者Watcher接收到相应属性的变化通知，就会执行对应的更新函数，从而去更新视图；
       
    核心：关于Vue双向数据绑定，核心是Object.defineProperty()方法或ES6 Proxy；

    Proxy对比Object.defineProperty()：
        场景更广泛，Proxy可直接监听数组类型的数据变化，以及可直接实现对象属性的新增/删除；
        功能更强大，Proxy可以劫持get、set、defineProperty、has、apply等13种属性，而defineProperty()只能劫持get和set属性；
        性能的提升，Proxy监听的目标为对象本身，不需要像Object.defineProperty一样遍历每个属性，有一定的性能提升；

###11. 单页面应用和多页面应用的区别及优缺点
    单页应用SPA只有一个主页面，浏览器一开始要加载全部的html,js,css。
    当路由跳转时，并不会真正地向服务端发出请求，而是通过js来切换局部组件，

    多页应用MPA具有多个主页面，浏览器一开始只会加载单个页面的html,js,css。
    在多个主页面之间跳转的时候，浏览器会向服务端发出请求以获取目标页面的资源，然后刷新整个页面；
    
    单页应用优点：整体响应速度快、服务器压力小、可实现复杂的过渡动画，数据管理较为方便（Vuex，Redux）；
    
    单页应用缺点：不利于SEO（可以使用SSR来优化），导航不可用（可自行建立路由栈管理），首屏渲染较慢；
###11. v-if和v-for的优先级
    在同一个元素上，v-for具有比v-if更高的优先级；
    如果在同一个DOM节点上使用，这意味着v-if将运行于每一个循环中，造成性能浪费，推荐的方案是吧v-if放在外层；
###12. assets和static的区别
    assets中的静态文件会被打包压缩进入index.html文件中；
    static中的资源文件不会经过打包压缩，而是直接上传到服务器；
###13. vue常用修饰符
    vue的修饰符包括事件修饰符、按键修饰符、系统修饰符三大类；

    1.事件修饰符：
        .stop: 相当于event.stopPropagation()，将会阻止事件的传播;
        .prevent：相当于event.preventDefault，将会阻止元素默认行为；
        .capture：添加事件监听器时使用捕获模式；
        .self：只当事件是从侦听器绑定的元素本身触发时才触发回调；
        .once：只会触发一次
        .passive - 告知浏览器继续元素的默认行为（相当于优化，常用于滚动监听）。

    关于passive: 浏览器只有等内核线程执行到事件监听器对应的js代码，才能知道内部是否需要调用preventDefault函数来阻止默认行为；
    所以浏览器本身是没办法对这种场景进行优化的，这种场景下用户的手势事件无法快速产生，会导致页面无法快速执行滑动逻辑，从而形成卡顿；
    通俗点说就是每次事件产生时，浏览器都会去查询一下是否有preventDefault，然后判断是否需要阻止事件的默认行为；
    我们加上passive就等同于直接告诉浏览器没有使用preventDefault，从而免去了查询这一步；
    passive一般用在滚动监听，因为滚动时会触发大量的事件，通过passive可以使内核线程跳过不必要的查询，从而提升页面交互的流畅度；
    
    2.按键修饰符：
        .enter
        .tab
        .delete
        .esc
        .space
        .up
        .down
        .middle
        .left：只当点击鼠标左键时触发。
        .right：只当点击鼠标右键时触发。
    
    3.系统修饰符
        .ctrl
        .alt
        .shift
        .meta
        .exact：修饰符允许你控制由精确的系统修饰符组合触发的事件

    2.v-modal修饰符
        .lazy：在默认情况下，v-model通过input事件触发来进行同步，你可以添加lazy修饰符，从而转为利用change事件同步；
        .number：自动将用户输入值转化为数值类型；
        .trim：自动过滤用户输入的收尾空格；
###14. Vue的两个核心点
    数据驱动：ViewModel，是指视图是由数据驱动生成的，我们对视图的修改，不会直接操作DOM，而是通过修改数据，保证了数据和视图的一致性；
    组件系统：组件的出现就是为了解决页面布局等等一系列问题，而vue中的组件分为两种，全局组件和局部组件，它提供了强大的页面布局功能。
###15. Vue和Jquery的区别
    jquery是使用选择器选取DOM对象，对其进行赋值、取值、事件绑定等操作；
    其实和通过原生的js操作html的区别只是在于可以更加方便的选取和操作DOM对象；

    Vue则是通过Vue对象将数据和View完全分离开来了，对数据进行操作不再需要直接引用相应的DOM对象，可以说数据和视图是分离的；
    数据和视图通过Vue对象这个vm实现相互的绑定，这就是MVVM框架的定义；
###16. SPA首屏加载慢的解决方法
    使用懒加载所需的资源；
    优化缓存；
    压缩静态资源；
    服务端渲染；
    优化CDN分发；
    使用骨架屏；
###17. Vue-router跳转和location.href跳转有什么区别
    使用location.href会向服务端发出请求，然后刷新整个页面；
    使用Vue-router不会向服务端发出请求，只是会更新路由状态；

    hash路由：通过监听hashchange事件，监听路由变化；
    history路由：通过调用history.pushState()方法改变路由的状态，以避免浏览器发出请求；
###18. 讲一下vue的插槽slot
    插槽用于控制组件的内容分发，通过插槽可以将DOM节点插入到组件内部的指定位置，从而使模板分块，实现模块化的特质和更大的重用性；
    其中，父组件控制插槽是否显示，如何显示，而子组件控制插槽的显示位置；

    基本用法：
        父组件：<TestDiv>Hello World</TestDiv>;
        子组件：<div><slot></slot></div>;
        则渲染时，子组件中的slot会被替换成'Hello World';

    作用域：
        父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的；
        (插槽可以访问与同一模板其余部分相同的实例property(即相同的“作用域”)，但不能访问被插入的组件中的实例property)；

    具名插槽：
        <slot>元素有一个特殊的属性：name，该属性的默认值为'default'，通过它可以实现在同一组件中渲染多个插槽；
        在向具名插槽提供内容时，可以使用v-slot指令确定插槽的名称；
        v-slot 只能添加在<template>上(只有一种例外情况，当被提供的内容只有默认插槽时，组件的标签才可以被当作插槽的模板来使用)。

        父组件：
            <TestDiv>
                <template v-slot:header>Hello World</template>
            </TestDiv>；
        子组件：
            <div>
                <slot name='header'></slot>
            </div>；

    作用域插槽：
        为了使插槽内容能够访问子组件中的数据，可以将任意数量的attrbute绑定到子组件<slot>中；
        然后在父组件中指定v-slot的值即为绑定的所有attrvute对象；
        
        父组件：
            <TestDiv>
                <template v-slot:header='defaultProps'>
                    {{defaultProps.author}}
                </template>
            </TestDiv>；
        子组件：
            <div>
                <slot name='header' author='Archie Li'></slot>
            </div>；
    
    注意：
        如果子组件中没有<slot></slot>，则父组件起始标签和结束标签之间的任何内容都会被抛弃；
        可以在在子组件中的<slot></slot>中写入备用内容，当父组件不提供插槽内容时，备用内容将会被渲染；
        默认插槽的缩写语法不能和具名插槽混用，因为它会导致作用域不明确；
        不带参数的 v-slot 被假定对应默认插槽：<TestDiv v-slot="slotProps">{{slotProps}}</TestDiv>；
        只要出现多个插槽，请始终为所有的插槽使用完整的基于 <template> 的语法；
        
        
###19. axios的特点有哪些
    从浏览器中创建XMLHttpRequests；
    node.js创建http请求；
    支持promise API；
    拦截请求和响应；
    转换请求数据和响应数据；
    取消请求；
    自动转换成JSON
    
    promise：一个对象用来传递异步操作的信息，promise的主要作用是解决回调地狱的问题，无需多次嵌套回调函数；
    本质：分离异步数据获取和业务；
###20. 请说下封装vue组件的过程
    1. 建立组件的模版，先写好页面的结构，样式；
    2. 准备好组件的数据输入，
    3. 准备好组件的数据输出，即根据组件逻辑，做好要暴露出来的方法；
    4. 封装完毕，直接调用即可；
###21. vue-router params和query的区别
    query需要通过path来引入，params需要通过name来引入，接受参数都是类似的：
    this.$route.query.name和this.$route.params.name
    url地址显示：query类似于ajax中的get传参数，parmas则类似于post传参；
    query刷新不会丢失query里面的数据，params刷新会丢失里面的数据；
###22. Vue初始化页面闪动问题
    浏览器自上而下解析Html文档，当文档挂载成功后，才会初始化Vue的app实例，然后将该实例挂载到DOM上；
    这两次挂载的过程很容易造成闪动现象，看到类似于{{message}}的字样，
    1. 可以在css里面加上[v-cloak]： {dispaly: none}；
    2. 如果没有彻底解决，则在根元素加上style="display: none;" v-bind:style="{display: 'block'}"；
###23. Vue常用组件库
    Element，Mint UI， VUX；
###24. 什么是vue生命周期？有什么作用；
    Vue生命周期指的是Vue实例从创建到销毁的一系列过程，包括开始创建、初始化数据、编译模版、挂载DOM，渲染，更新，销毁；

    Vue会运行不同的生命周期钩子函数，用户可以在这些函数中添加自己的代码；

###25. 第一次页面加载会触发哪几个钩子；
    beforeCreate， createed, beforeMount, mounted;
###26. Vue生命周期（常用）
    beforeCreate: 
        在实例初始化之后、进行数据侦听和事件/侦听器的配置之前同步调用。
    created：
        在实例创建完成后被立即同步调用。此时实例已完成对选项的处理，以下内容已被配置完毕：数据侦听、计算属性、方法、事件/侦听器的回调函数。
        然而，挂载阶段还没开始，且 $el property 目前尚不可用，如果要想和DOM进行交互，可以通过vm.$nextTick来访问DOM；
        网络请求最早可以在这个阶段中进行；
    beforeMounted:
        在挂载开始之前被调用：相关的 render 函数首次被调用。
        执行到这个钩子的时候，在内存中已经编译好了模版了，但是还没有挂载到页面中；
        （编译模版：利用data中的数据和模版生成html文档，注意此时html还未挂载到页面上）
    mounted: 
        在组件被挂载之后被调用（el被新创建的vm.$el替换）；
        在这一阶段，真实的DOM挂载完成，数据完成双向绑定，可以访问DOM节点；
        注意 mounted 不会保证所有的子组件也都被挂载完成。如果你希望等待整个视图都渲染完毕，可以在 mounted 内部使用 vm.$nextTick；
        （这一阶段将会利用上面编译好的html内容替换el属性指向的DOM对象，渲染到页面上）
    beforeUpdate: 
        在数据发生改变后，DOM被更新之前被调用；
        发生在虚拟DOM重新渲染和打补丁（patch）之前，也就是说，当执行这个钩子时；
        页面显示的数据还是旧的，而data中的数据是更新后的，页面还没有和最新的数据保持同步；
        可以在这个钩子中进一步更改状态，这不会触发附加的重渲染过程；
    updated: 
        在数据更改导致的虚拟 DOM 重新渲染和更新完毕之后被调用。
        页面显示的数据和data中的数据已经保持同步了，都是最新的；
        这一期间应当避免再次更新数据，因为这样可能导致无限循环的更新；
        注意，updated 不会保证所有的子组件也都被重新渲染完毕。如果你希望等待整个视图都渲染完毕，可以在 updated 内部使用 vm.$nextTick；
    beforeDestory:
        在卸载组件实例之前调用。在这个阶段，实例仍然是完全正常的；
        可以在这个时候清除定时器等；
    destoryed: 
        卸载组件实例后调用。组件实例的所有指令都被解除绑定，所有事件侦听器都被移除，其内部所有子组件实例被卸载。
        这个时候所有的data, methods, 指令，过滤器等都是不可用状态；
###27. Vue生命周期（不常用）
    activated: keep-alive专属，组件被激活时调用；
    deactivated: keep-alive专属，组件失活时调用；
    errorCaptured: 在捕获一个来自后代组件的错误时被调用，此钩子可以返回 false 以阻止该错误继续向上传播；
    renderTracked: 跟踪虚拟 DOM 重新渲染时调用，此事件告诉你哪个操作跟踪了组件以及该操作的目标对象和键；
    renderTriggered: 当虚拟DOM重新渲染被触发时调用，此事件告诉你是什么操作触发了重新渲染，以及该操作的目标对象和键；
###27. created和mounted的区别
    created之后还未开始编译模版，而mounted之后已经完成模版编译并且完成了组件的挂载；
    简单来说，created之后不能立即访问DOM，而mounted之后可以访问DOM；
###28. vue异步请求一般是在哪个周期函数；
    可以在created/beforeMounted/mounted中进行异步请求；
    因为在这三个钩子函数中，实例已完成对选项的处理（数据侦听、计算属性、方法、事件/侦听器的回调函数等都已经被配置完毕），可以根据服务端返回的数据更新组件状态；
    
    如果异步请求不需要依赖DOM，推荐在created钩子函数中进行异步请求，能够更快获取到服务端数据，减少页面loading时间；
    但是如果要操作DOM，那么肯定是在mounted的时候进行；
###29. 请详细说下你对Vue生命周期的理解；
    8个常用阶段： beforeCreated/created，beforeMounted/mounted，beforeUpdate/updated，beforeDestory/destoried；
    5个不常用阶段： activated/deactivated，errorCaptured，renderTracked，rendertriggered；

###30. mvvm框架是什么
    vue是实现了双向数据绑定的mvvm框架，当视图View改变时更新模型层，当模型层改变的时候更新视图层；
###31. vue-router是什么，它有哪些组件
    vue-router是一个用来写路由的库，包括router-link、router-view等组件；
###32. $route 和 $router的区别
    $router是VueRouter的实例，在script标签中想要导航到不同的URL，使用$router.push方法
    $route是当前的router跳转对象，里面可以获取当前路由的name, path, query, params等；
###33. vue-router的两种模式
    1. hash模式：
        基于url的hash值，hash虽然出现于URL中，但改变url的hash值不会触发新的Http请求；
        通过监听window对象的hashchang事件控制页面的渲染逻辑；
    2. history模式:
        基于history对象中新增的pushState() 和 replaceState方法()
        这两个方法应用于浏览器的历史记录栈，在当前已有的back，forward，go的基础上，它们提供了对历史记录进行修改的功能；
        当调用他们修改浏览器历史记录栈后，虽然当前URL改变了，但浏览器不会刷新页面，这就是history模式"更新视图但不更重新请求页面"的原理。

        但由此也会导致一个问题，即url此时并不代表服务器上对应位置的资源，而是一种状态，所以会出现刷新后404的问题；
        需要服务端或Nginx进行相关配置，增加一个覆盖所有情况的候选资源，如果url请求不到，则返回前端项目的index.html文件；
###35. vuex是什么？哪种功能场景使用它
    vuex是一个专门为vue.js应用程序开发的的状态管理库，可以帮助我们共享状态，也就是管理全局变量；
    vuex使用一个store对象来管理应用的状态，一个store包括：state，getter，action，mutation四个属性；
    另外，当store对象过于庞大时，可以根据具体的业务需求分为多个module
    
    具体工作流程为：在组件中触发action，action则会提交mutation，然后mutation对state进行修改，最后组件再根据state， getter渲染页面；
###36. vuex有哪几种属性
    有5种，分别是state, getter, mutation, action, module
    state: 用于存放数据源；
    getter: 从数据源中派生出来的数据
    mutation: mutation是vuex中改变state的唯一途径，并且只能同步操作；
    action: 一些对state的异步操作可以放在action中，并在action中通过提交mutations来更新state；
    module: 当store对象过于庞大时，可以根据具体的业务需求分为多个module；
###38. MVC和MVVM的区别
    1. MVC全名model-View-Controller(模型-视图-控制器)，一种软件设计典范；
        Model: 是用于处理应用程序数据逻辑部分，通常模型对象负责在数据库中存取数据；
        View: 是应用程序中处理数据显示的部分，通常视图是依据模型数据创建的；
        Controller: 是应用程序处理用户交互的部分，通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据；
      MVC思想：一句话描述就是Controller负责将Model的数据用View显示出来（Controller把model的数据交给View）；
    2. MVVM新增了VM类（ViewModel层），
        ViewModel层：通过两件事做到了数据的双向绑定：
        一是将【模型】转化为【视图】，即将后端传递的数据转化成所看到的页面，实现的方式是：数据绑定；
        二是将【视图】转化为【模型】，即将所看到的页面转化成后端的数据，实现的方式是：DOM事件监听；
    3. MVC和MVVM的最大区别就是：实现了View与Model的自动同步，也就是说当Model的属性发生的时候，我们不再需要手动地
        去操作DOM元素来改变View的显示，二是改变属性后该属性对应的View层显示会自动改变（对应Vue数据驱动的思想）
        整体来看，MVVM比MVC精简了许多，不仅简化了业务与界面的依赖，还解决了数据频繁更新的问题，不用再用选择器来操作DOM元素；
        因为在MVVM中，View不知道Model的存在，Model和ViewModel也察觉不到View，这种低耦合模式提高了代码的可重用性；
        注意：Vue并没有完全遵循MVVM的思想；
        
    简单理解：
        传统的MVC：
            数据只能由View => Controller => Model => View这样循环；
            例如：用户键盘输入后，视图层View发生改变，但是数据层Model无法立即响应，必须要在Controlle设置监听器，告知Model执行相关操作；
        MVVM：
            数据流动类似于：View <=> ViewModel <=> Model
            数据View的变动，可以直接反应在ViewModel中，然后ViewModel将数据自动同步到Model    
###39. 为什么官方要说Vue没有完全遵循MVVM思想
    严格的MVVM要求View不能和Model直接通信，而Vue则提供了$refs这个属性，让Model可以直接操作View，这违背了MVVM的思想；

###38. vue组件通讯有哪些方式
        1. $props和$emit: 父组件通过$props向子组件传递数据，子组件通过$emits调用父组件中绑定(v-on)的事件；
        2. $parent和$children：分别用于获取当前组件的父组件，当前组件的子组件；
        3. $attr：获取父作用域中非Prop的Attribute（组件内部并没有相应props或emits定义的attribute）；
        4. $refs：获取DOM节点或组件实例；
        5. provide/inject：父组件通过provide选项来提供变量，然后在子组件中通过inject选项来注入变量。
        6. vuex全局状态管理；
        7. eventBus兄弟组件数据传递，这种情况下可以使用事件总线的方式；
###40. 如何理解Vue的单向数据流
    1. 数据总是从父组件传递到子组件，即子组件通过props选项接受父组件传递的状态；
    2. 子组件没有权利修改父组件传过来的数据，只能请求父组件对原始数据进行修改（子组件通过$emit触发父组件通过v-on绑定的方法）；
    这样可以防止因子组件意外改变父组件的状态，而导致应用数据流向难以理解；
    
    注意：在子组件中直接使用v-modal绑定父组件传过来的props是不规范的写法，开发情况会报警告；

###42. vue如何检测数组变化
    数组考虑性能原因没有用 defineProperty 对数组的每一项进行拦截，而是选择对7种数组（push,shift,pop,splice,unshift,sort,reverse）方法进行重写（AOP 切片思想）。
    
    所以在 Vue 中修改数组的索引和长度无法监控到。需要通过以上7种变异方法修改数组才会触发数组对应的watcher进行更新。   
###43. vue3.0了解过吗
    1. 响应式原理的改变：Vue3.x使用Proxy取代Vue2.x版本的Object.defineProperty；
    2. 组件选项声明方式：Vue3.x使用Compositoin API； setup是Vue3.x新增的一个选项，他是组件内部使用Composition Api的入口；
    3. 模版语法变化：slot具名插槽语法，自定义指令v-model升级;
    4. 其他方面的更改 Suspense支持Fragment（多个根节点）和 Protal（在dom其他部分渲染组件内容）组件，针对一些特殊的场景做了处理。基于 treeShaking 优化，提供了更多的内置功能。
###44 Vue3和Vue2响应式原理的区别
    Vue3.x改用了Proxy代替Object.defineProperty，因为Proxy可以直接监听对象和数组的变化，并且有多达13中拦截方法；
###45. Vue父子组件生命周期钩子函数执行顺序
    1. 加载渲染过程：
        父beforeCreate => 父created => 父beforeMount => 子beforeCreated => 子created => 子beforeMounted => 子mounted => 父mounted
    2. 子组件更新过程    
        父beforeUpdate => 子beforeUpdate => 子updated => 父updated 
    3. 父组件更新过程
        父beforeUpdate => 父updated
    4. 卸载过程：
        父beforeDestroy -> 子beforeDestroy -> 子destroyed -> 父destroyed
###46. 虚拟DOM是什么，有什么优缺点
    由于在浏览器中操作DOM是非昂贵的，频繁操作DOM，会产生一定的性能问题，这就是虚拟DOM的产生原因；
    虚拟DOM的本质就是用原生的JS对象去描述DOM节点和DOM树结构，是对真实DOM的一层抽象；
    
    原理：
        1. 在组件渲染的时候会调用render函数，这个函数会生成一个虚拟DOM，再根据这个虚拟DOM生成真实的DOM；
           然后这个真实的DOM会挂载到我们的页面中；
        2. 如果组件内有响应的数据，数据发生改变的时候render函数会生成一个新的虚拟DOM；
           然后将新的虚拟DOM树和旧的虚拟DOM树进行对比，找到要要修改的虚拟DOM的部分，去修改相对应部分的真实DOM；
    
    优点：
        1. 保证性能下限：框架的虚拟DOM需要适配任何上层API可能产生的操作，它的一些DOM操作的实现必须是普适的，所以它的性能不是最优的；
           但是比起粗暴的DOM操作性能要好很多，因此框架的虚拟DOM至少可以保证你在不需要手动优化的情况下，还能拥有不错的性能，即保证性能下限；
        2. 无需手动操作DOM：我们只需要写好View-Model层的代码逻辑，框架会根据虚拟DOM和双向数据绑定，帮助我们以可预期的方式更新视图，极大地提高我们的开发效率；
        3. 跨平台，虚拟DOM的本质是javascript对象，而real DOM与平台强相关，相比之下虚拟DOM可以更加便捷地进行跨平台操作，比如服务端渲染，weex开发等；
    
    缺点：
        1. 首次渲染大量DOM的时候，由于多了一层DOM计算，会比innerHTML插入慢；   
        2. 如果只是渲染一个页面后期不改动的话 那么虚拟 dom 其实成本更高 因为 都要渲染成真实的 dom  
###46. 对虚拟DOM的理解
    https://blog.csdn.net/weixin_44059045/article/details/121824936
    从本质上来说，Virtual DOM是一个JavaScript对象，这个对象是更加轻量级的对真实DOM的描述；
    通过对象的方式来表示DOM结构，将页面的状态抽象为JS对象的形式；
    通过事务处理机制，将多次DOM修改的结果一次性的更新到页面上，从而有效的减少页面渲染的次数，以及DOM的重绘重排次数，提高渲染性能；

    在代码渲染到页面之前，vue会把代码转换成一个对虚拟DOM，然后以对象的形式来描述真实DOM结构，最终将真实DOM渲染到页面上；
    在页面状态发生变化后，虚拟DOM会将多次DOM修改产生的新虚拟DOM，与之前缓存的旧虚拟DOM进行diff比较；
    通过diff算法，Vue会计算出发生改变的部分，然后将发生改变的部分应用到真实DOM，并渲染到页面上；
    
    虚拟DOM设计的最初目的，就是更好的跨平台，比如Node.js就没有DOM，为了实现SSR借助虚拟DOM，因为虚拟DOM本身是js对象。

    现代前端框架的一个基本要求就是无须手动操作DOM，因为手动操作DOM无法保证程序性能，并且手动操作DOM的开发模式效率低下。

###46. 虚拟DOM的解析过程
    https://blog.csdn.net/weixin_44059045/article/details/121824936
    首先对模版编译后的数据进行分析，然后用js对象（虚拟DOM）将整个DOM树表示出来，这个对象将包含TagName、Props和Children这些属性，
    然后将这个js对象树给保存下来，并将其映射到真实DOM。

    当页面的状态发生改变，导致需要对页面的DOM的结构进行调整时，首先Vue会根据变更的状态，重新构建起一棵js对象树，
    然后将这棵新的js对象树和旧的js对象树进行比较，记录下两棵树的的差异。
    
    最后将记录的有差异的地方应用到真正的DOM树中去，这样视图就更新了；

###46. 虚拟DOM真的比真实DOM性能好吗
    真实DOM：生成HTML字符串＋重建所有的DOM元素；
    虚拟DOM：生成vNode+ DOMDiff＋必要的dom更新；

    首次渲染大量DOM时，由于多了一层虚拟DOM的计算，会比innerHTML插入慢。
    其他情况下，比如数据更新后重新渲染时，还是比真实DOM快很多的；

###47. Diff算法的原理
    https://blog.csdn.net/weixin_44059045/article/details/121824936
    在新老虚拟DOM对比时：
    1. 首先，对比节点本身，判断是否为同一节点，如果不为相同节点，则删除该节点重新创建节点进行替换
    2. 如果为相同节点，进行patchVnode，判断如何对该节点的子节点进行处理，先判断一方有子节点一方没有子节点的情况(如果新的children没有子节点，将旧的子节点移除)
    3. 比较如果都有子节点，则进行updateChildren，判断如何对这些新老节点的子节点进行操作（diff核心）。
    4. 匹配时，找到相同的子节点，递归比较子节点
    
    在diff中，只对同层的子节点进行比较，放弃跨级的节点比较，使得时间复杂从O(n3)降低值O(n)，也就是说，只有当新旧children都为多个子节点时才需要用核心的Diff算法进行同层级比较。
    
###47. Vue中Key的作用
    todo.archie https://blog.csdn.net/weixin_44059045/article/details/121824936
    Vue中的key可以分为两种情况来考虑：
    1. v-if: 
        由于Vue会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染，因此当使用v-if来切换元素时，
        如果切换前后DOM树相同位置上有相同类型的元素，那么这个元素将会被复用；而如果是相同的input元素，那么切换前后用户的输入不会被清除掉，
        因此可以通过key来唯一标识一个元素，这样使用key的元素不会被复用，此时key的作用就相当于元素的唯一标识；
    2. v-for:
        当需要更新使用v-for渲染出来的列表时，Vue会默认采用"就地更新"的策略，也就是说如果数据项的顺序发生了改变，
        Vue不会移动虚拟DOM节点来匹配数据项的顺序，而是简单地复用相同位置上的元素，因此可以给每个列表项提供一个key，
        以便Vue来跟踪元素的身份，从而实现高效的复用，这个时候key的作用是为了高效地更新虚拟DOM；

    使用index作为key相当于不写key，因为无论数组颠倒，index都是0，1，2，3这样递增的；如果数组顺序变化引起更新，则导致Vue复用错误的子节点；
    
###47. v-modal的原理
    v-modal本质上是一个语法糖（指在现有js语言语法和功能的基础上，增加了一些代码逻辑和使用规则，从而更方便程序员使用。）    
    可以用 v-model 指令在表单 <input>、<textarea> 及 <select> 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。
    
    v-modal在内部为不同的输入元素使用不同的property并抛出不同的事件；
        1. input text和textarea元素监听input事件，并返回value属性的值；     
        2. intput checkbox和input redio元素监听change事件，并返回chcked属性的值；
        3. select监听change事件，并返回value属性得的值；

###48. Vue事件绑定原理
    Vue中通过v-on或其语法糖@指令来给元素绑定事件并且提供了事件修饰符，基本流程是：
        1. 进行模板编译生成AST（抽象语法树），
        2. 生成render函数后并执行得到VNode（虚拟节点）；
        3. VNode生成真实DOM节点或者组件时候使用addEventListener方法进行事件绑定。

###49. vue-router路由钩子函数是什么？执行顺序是什么？
    钩子函数的种类有：全局守卫、路由守卫、组件守卫；

    全局守卫：
        全局前置守卫（router.beforeEach）；
        全局解析守卫（router.beoreResolve）；
        全局后置钩子（router.afterEach）；
    路由守卫：
        直接在路由配置上定义 beforeEnter 守卫；
    组件守卫：
        beforeRouteEnter（在渲染该组件的对应路由被验证前调用，不能获取组件实例this）；
        beforeRouteUpdate（在当前路由改变，但是该组件被复用时调用）；
        beforeRouteLeave（在导航离开渲染该组件的对应路由时调用）；
    
    完整的导航解析流程：
        1. 导航被触发。
        2. 在失活的组件调用beforeRouterUpdate守卫；
        3. 调用全局的beforeEach守卫；
        4. 在重用的组件里调用beforeRouteUpdate守卫；
        5. 在路由配置里调用beforeEnter；
        6. 解析异步路由组件；
        7. 在被激活的组件里调用beforeRouteEnter；
        8. 调用全局beforeResolve守卫；
        9. 导航被确认；
        10. 调用全局的afterEach钩子；
        11. 触发DOM更新；
        12. 调用beforeRouteEnter守卫中传给next的回调函数，创建好的组件实例会作为回调函数的参数传入；
###50. vue-router动态路由匹配
    当需要将给定匹配模式、但携带信息的路由映射到同一个组件时，我们可以在路径中使用一个动态字段，这个字段称之为路径参数；

    路径参数用冒号: 表示。当一个路由被匹配时，它的参数值将在每个组件中以this.$route.params的形式暴露出来。
    
###51. vue-router路由懒加载
    component(和components)配置接收一个返回Promise组件的函数，比如：() => import('./TestComponent')；
    Vue Router只会在第一次进入页面时才会获取这个函数，然后使用缓存数据；
    这意味着你也可以使用更复杂的函数，只要它们返回一个 Promise；

###51. vue-router动态路由
    动态路由主要通过两个函数实现。
    
    查询路由：router.hasRoute()：检查路由是否存在；
    获取路由：router.getRoutes()：获取一个包含所有路由记录的数组；
    增加路由：router.addRoute()；
    删除路由：router.removeRoute(temp)，其中temp为调用 router.addRoute() 返回的回调；

    注意：如果新增加的路由与当前位置相匹配，就需要你用 router.push() 或 router.replace() 来手动导航，才能显示该新路由。

###51. 谈一下对vuex的理解
    Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式 + 库；
    它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

    主要包括以下几个模块：
        State：定义了应用的单一状态树，通过一个对象用表示全部的应用层级状态，并利用mapState()辅助函数映射到组件的计算属性；
        Getter：可以通过Getter从全局状态中派生出一些状态，并利用mapGetters()辅助函数映射到组件的计算属性；
        Mutation：
            更改全局状态的唯一方法是通过store.commit('temp')提交mutation，并且mutation处理函数必须是同步函数；
            可利用mapMutations辅助函数将组件的methods映射为store.dispatch调用；
        Action：
            可以利用store.dispath('temp')提交mutation，而不是直接变更状态；
            可以在actions处理函数中包含任意异步请求，然后提交mutation；
            可利用mapMutations辅助函数将组件的methods映射为store.dispatch调用；
        Module：允许将单一的Store拆分更多个store且保存在单一的状态树中；

###52. Vuex页面刷新数据丢失怎么解决
    1. 重新请求服务器获取数据，动态更新；
    2. 数据持久化，一般使用本地存储的方案来保存数据（cookie，localStorage，sessionStorage，indexDB等）
###53. Vuex为什么要分模块并且加命名空间；
    模块化：由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。
    命名空间：是为了解决方法可能出现mutation/action命名重复的问题；

###54. 使用过SSR吗
    SSR也就是服务端渲染，也就是将React，Vue在客户端把标签渲染成HTML的工作放在服务端完成，然后把html直接返回给客户端
    优点：SSR有着更好的SEO，并且首屏加载速度更快
    缺点：服务端渲染应用程序需要处于node.js运行环境，并且会让服务器有更大的负载需求；
###55. vue中使用了哪些设计模式
    工厂模式：传入参数即可以创建实例，虚拟dom根据参数的不容返回基础标签的Vnode和组件Vnode；
    单例模式：整个程序有且仅有一个实例；   
    发布订阅模式：vue事件机制
    观察者模式：响应数据原理
###56. Vue性能优化
    不需要响应式的数据不要放在data中，可以使用Object.freeze()冻结数据；
    v-if和v-show区分使用场景；
    computed和watch区分场景使用；
    v-for必须加上key，并且v-for中避免使用v-if；
    大数据列表和表格性能优化：虚拟列表 / 虚拟表格；
    防止内部泄漏，组件销毁前将全局变量和定时器销毁；
    图片懒加载；
    路由懒加载；
    异步路由；
    第三方插件按需加载；
    适当采用keep-alive缓存组件；
    防抖节流的运用；
    服务端SSR或者预渲染；
###57 mixin的使用场景和原理
    使用场景：Mixin可以用来分发Vue组件中的可复用功能，比如某些组件在挂载前或挂载后需要执行一些相同的副作用（网络请求等）；
    原理：一个mixi 对象可以包含任意组件选项，当组件使用这个mixin对象时，其中的选项将被“混合”进入该组件本身的选项。

    app.mixin({...}) 表示注册一个全局的mixin，注意它会影响之后注册的每一个组件，因此不太推荐使用；
###60. 有写过自定义指令吗，原理是什么
    指令本质上是装饰器，是vue对HTML元素的拓展，给HTML元素添加自定义功能，vue编译DOM的时候，会找到指令对象，执行指令的相关方法；
    
    自定义指令有7个钩子函数，分别是created, beforeMount/mounted, beforeUpdated/updated, beforeUnmount/unmounted
        1.created：在绑定元素的 attribute 或事件监听器被应用之前调用。在指令需要附加在普通的 v-on 事件监听器调用前的事件监听器中时，这很有用。
        2.beforeMount：当指令第一次绑定到元素并且在挂载父组件之前调用。
        3.mounted：在绑定元素的父组件被挂载后调用。
        4.beforeUpdate：在更新包含组件的 VNode 之前调用。
        5.updated：在包含组件的 VNode 及其子组件的 VNode 更新后调用。
        6.beforeUnmount：在卸载绑定元素的父组件之前调用
        7.unmounted：当指令与元素解除绑定且父组件已卸载时，只调用一次。

    自定义指令的钩子函数都有四个参数： el、binding、vnode 和 prevVnode
        1.el：指令绑定到的元素。这可用于直接操作 DOM
        2.binding：一个包含以下属性的对象
            instance（使用指令的组件实例），
            value（传递给指令的值），
            oldValue（先前的值），
            arg（传递给指令的参数(如果有的话)），
            modifiers（包含修饰符(如果有的话) 的对象），
            dir（一个对象，在注册指令时作为参数传递）
        3.vnode：一个真实 DOM 元素的蓝图，对应上面收到的 el 参数。
        4.prevVnode：上一个虚拟节点，仅在 beforeUpdate 和 updated 钩子中可用。
    
    原理：Vue指令解析和生效分为三个阶段：模板编译阶段， 生成VNode阶段， 以及生成真实Dom的patch阶段
        1.模版编译阶段：
        2.生成vNode阶段：
        3.生成真实Dom的patch阶段：

    1. 在生成ast语法树的时候，遇到指令会给当前元素添加directives属性
    2. 通过genDirectives生成指令代码
    3. 在patch前将指令的钩子提取到cbs中，在patch过程中调用对应的钩子；
    4. 当执行指令对应的钩子函数时，调用对应指令的自定义方法

###62. vue指令编译原理
    https://blog.csdn.net/comedyking/article/details/115551173

    Vue有自带编译器的版本和不带编译器的版本，即runtime +complier 和 runtime 版本。
    编译器的主要作用是将.vue的模板编译为render函数，在开发的时候，写render函数不符合我们的开发习惯，所以我们平常开发用的都是自带编译器的版本。
    而项目打包时，编译的工作将交由webpack来执行打包编译完成，这样就不需要vue自带的编译器了。

    Vue的模板编译过程其实就是将 模板template内容 转换为 render函数的过程。主要分为3个流程：
        1、将模版字符串转为ast抽象语法树。ast语法树就是描述dom树形结构的对象。如描述dom节点的类型，标签，属性，子元素等；
        2、优化ast抽象语法树。主要是标记一些节点内容不变的节点为静态节点和静态根节点，patch更新对比时会跳过这些节点的比对和重新渲染；
        3、生成render方法。将优化好的ast语法树。通过递归的方式，拼接为render方法的字符串，最后执行通过new Function(str)转为render方法；

    Runtime+Complier版本的渲染流程:
        1. vue complier将模板字符串转为ast抽象语法树...
        2. 优化ast抽象语法树。
        3. 生成render方法。
        4. render函数将生成对应的虚拟dom，VNode。
        5. 在组件patch阶段，将生成的VNode生成真实dom元素，添加/更新到dom树上。

###62. Vue模版编译原理
    Vue的编译过程就是将template转化成render函数的过程，分为以下三步：
        1. 第一步将模版字符串转化成element ASTs(解析器)
        2. 第二步是对AST进行静态节点标记，主要用来做虚拟DOM的渲染优化（优化器）
        3. 第三步是使用element AST生成render函数代码字符串（代码生成器）
###63. 生命钩子是如何实现的
    Vue的生命周期钩子核心实现是利用发布订阅模式先把用户传入的生命周期钩子订阅好（内部采用数组的方法存储）；
    然后在创建组件实例的过程中会一次执行对应的钩子方法（发布）；
###77. 双向绑定
    1. 什么是双向绑定?
        我们先从单向绑定切入，单向绑定非常简单，就是把Model绑定到View，这样，当我们用JavaScript代码更新Modal时，View就会自动更新；
        双向绑定就是在单向绑定的基础上，用户更新了View，Modal的数据也自动更新了，这种情况就是双向绑定
        比如，当用户填写表单时，View的状态会随着用户的输入而发生改变，而如果此时可以自动更新Model的状态，那就相当于我们把Model和View进行了双向绑定；
    2. 双向绑定的原理是什么
       Vue是实现了MVVM架构思想的JS框架，而MVVM由三个部分构成：
            数据层（Model）：代表数据模型，可以在Model中定义数据修改和操作的业务逻辑；
            视图层（View）：负责将数据模型转化成UI展现出来；
            业务逻辑层（ViewModel）：框架封装的核心，他负责将数据和视图关联起来；
                用于监听数据模型的改变同时控制视图的行为、处理用户交互；
                简单理解就是一个同步Model和View的对象；
       
       这里业务逻辑层的核心功能便是数据双向绑定，ViewModel的职责是：
            数据变化后更新视图；
            视图变化后更新数据；             
       
       ViewModel由两个主要部分组成：
            监听器：对所有数据的属性进行监听
            解析器：对每个元素节点的指令进行扫描跟解析，根据指令模版替换数据，以及绑定相应的更新函数；     
    
       ViewModel通过数据双向绑定把View层和Model层连接了起来，而View和Model之间的同步工作完全是自动的，无需人为干涉；
       因此开发者只需要关注业务逻辑，不需要手动哦操作DOM，不需要关注数据状态的同步问题，复杂的数据状态维护由MVVM来统一管理；
    
    3. 如何实现双向绑定
        在Vue中，双向绑定的流程是：
            1. new Vue()首先执行初始化，对data执行响应化处理，这个过程发生在Obsserve中，defineReactive时为每个key创建一个Dep实例；
            2. 同时对模板执行编译，找到其中动态绑定的数据，从 data 中获取并初始化视图，这个过程发生在 Compile 中；初始化视图时读取某个 key，例如 name1，创建⼀个 watcher1
            3. 同时定义⼀个更新函数和 Watcher，将来对应数据变化时 Watcher 会调用更新函数
            4. 由于 data 的某个 key 在⼀个视图中可能出现多次，所以每个 key 都需要⼀个管家 Dep 来管理多个 Watcher;由于触发 name1 的 getter 方法，便将 watcher1 添加到 name1 对应的 Dep 中
            5. 将来 data 中数据⼀旦发生变化,会首先找到对应的 Dep，通知所有 Watcher 执行更新函数；当 name1 更新，setter 触发时，便可通过对应 Dep 通知其管理所有 Watcher 更新
           
            实现思路
            
            defineReactive 时为每⼀个 key 创建⼀个 Dep 实例
            初始化视图时读取某个 key，例如 name1，创建⼀个 watcher1
            由于触发 name1 的 getter 方法，便将 watcher1 添加到 name1 对应的 Dep 中
            当 name1 更新，setter 触发时，便可通过对应 Dep 通知其管理所有 Watcher 更新
### 78. vue的路由拦截器（导航守卫）的作用
    例如：权限设置，当用户没有登录权限的时候就会跳转到登录页面；
    
### 82. 什么是Vue的计算属性
    在模版中放入太多的逻辑会让模版过重并且难以维护，在需要对数据进行复杂处理的时候，且可能需要多次使用的情况下；可以采取计算属性的方式：
    好处：
        1. 使得数据处理逻辑更加清晰
        2. 依赖于数据，数据更新，处理结果自动更新
        3. 计算属性内部this指向vm实例
        4. 相比于methods，不管依赖的数据变不变，methods都会重新计算，
            但是依赖数据不变的时候，computed将会直接从缓存中获取，不会重新计算；
### 83. 聊聊你对Vue.js的模版编译的理解
    简而言之，就是先转化为AST树，再得到渲染函数返回VNODE（Vue的虚拟DOM节点）
    
    详细步骤：
        首先，通过编译器将模版编译成AST树（抽象语法树即源代码的抽象语法结构的树状表现形式），
        编译是createCompiler的返回值，createComopiler是用以创建编译器的，负责合并选项；
        
        然后，AST会经过（将AST语法树转化成渲染功能字符串的过程）得到渲染函数，渲染的返回值是VNode，
        VNode是Vue的虚拟DOM节点，里面有（标签名，子节点，文本等）；  
        
### 84. vue与react的区别
    相同点：
        1. 都鼓励组件化；
        2. 都有props的概念，都有自己的构建工具；
        3. React与Vue只有框架的骨架，其他的功能模块如路由、状态管理等是框架分离的组件；
    不同点：
        1. React是单向数据流，而Vue是数据双向绑定；
        2. React使用JSX，而Vue使用HTML模版；
        3. React的状态保存在state中，使用setState更新，而Vue中的数据保存在data属性中，可以直接操作；
### 86. vue style绑定class的数组用法
    1. 对象方法： v-bind:class="{'class1': isShow, 'class2': isShow2}"；
    2. 数组方法： v-bind:class="[class1, class2]"；
    3. 行内样式： v-bind:style="{color: color, fontSize: fontSize + 'px'}"
### 87. computed 与 watch 的区别
    计算属性是自动监听依赖值的变化，从而动态返回内容，而监听是一个过程，在监听的值发生变化时，可以触发一个回调，在回调中处理业务逻辑；
    两者最大的区别来源于用法：
        1. 只要是需要返回动态值，那么就使用计算属性；
        2. 如果是需要在值发生改变之后执行业务逻辑，那么就使用watch；
    
    相关拓展：
    1. computed是一个对象时，它有哪些选项？
        有get和set两个选项
    
    2. computed 和 methods 有什么区别？
        methods是一个方法，它可以接受参数，而computed不能，computed是可以缓存的，methods不能；
    
    3. computed 是否可以依赖其他组件的数据
        computed可以依赖于其他computed，甚至是其他组件的data；
        
    4. watch是一个对象时，它有哪些选项
        watch配置，handler，deep是否深度，immeditate是否立即执行
        
    总结：当有一些数据需要随着另外一些数据变化时，建议使用computed；
        当有一个通用的响应数据变化的时候，要执行一些业务逻辑或者异步操作的时候，建议使用watcher；

### 89. 组件间的通信
    1. 父子：props/event, $parent/$children, ref, provide/inject；
    2. 兄弟：bus, vuex
    3. 跨级：bus, vuex, provider/inject

### 90. vue的原理
    Vue的模式是m-v-vm模式，通过modelView作为中间件（即vm的实例），进行数据双向绑定；
    过程：
        1. 通过建立虚拟DOM树document.createDocumentFragment()，方法创建虚拟DOM树；
        2. 一旦被检测的数据改变，会通过Object.defineProperty定义的数据拦截，截取到数据的变化；
        3. 读取截取到的数据变化，从而通过订阅-发布模式，触发Watcher（观察者），从而改变虚拟DOM的具体数据；
        4. 最后，通过更新虚拟DOM的元素值，从而改变卒后渲染DOM树的值，完成双向绑定；
### 91. 理解Vue中的Render渲染函数
    vue一般使用template来创建html，然后在有的时候，我们需要使用javascript来创建html，这个时候我们就需要render函数；
    
    render函数返回一个createElement组件中的子组件，存储在组件实例¥slots.default中；     

### 92. vue事件如何在内联语句使用event对象
    利用特殊变量$event：
    <button v-on:click="Event($event)">chick</button>
    
### 94. is的用法
    todo.archie
### 95. vue-router如何响应 路由参数 的变化？
    使用watch监听当前路由的参数（this.$route.params）；
    利用beforeRouteUpdate导航守卫；
### 95. vue-router传递参数的几种方式
    vue-router传递参数主要分为两大类：编程式的导航和声明式的导航

    编程式导航：
        router.push({
            path: '/test',
            params: { name: 'archie' },
            query: { age: 22 },
            hash: 'part1'
        })

    声明式导航：
        <router-link v-bind:to="{path: '/test', params: {name: 'archie'}, query: {age: 22}}" replace></router-link>
### 95. vue-router如何定义嵌套路由？
    在路由配置中通过children属性定义；
### 95. <router-link>组件及其属性
    router-link是一个自定义组件，用来表示一个链接，可以实现在不重新加载页面的情况下更改或处理URL。

    所有属性：
       to：表示目标路由的链接。当被点击后，内部会立刻把 to 的值传到 router.push()；
       replace：设置replace属性的话，当点击时，会调用router.replace()，而不是 router.push()，导航后不会留下历史记录；
       active-class：链接激活时，应用于渲染的 <a> 的 class。
       aria-current-value：当链接激活时，传递给属性 aria-current 的值。
       custom：
            <router-link> 是否应该将其内容包裹在 <a> 元素中。在使用 v-slot 创建自定义 RouterLink 时很有用。
            默认情况下，<router-link> 会将其内容包裹在 <a> 元素中，即使使用 v-slot 也是如此。
            传递自定义的 prop，可以去除这种行为。
       exact-active-value：链接精准激活时，应用于渲染的 <a> 的 class。











