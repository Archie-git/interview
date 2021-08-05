###1. Vue的优点
    1. 轻量级框架：只关注视图层，是一个构建数据的视图集合，大小只有几十kb；
    2. 简单易学：国人开发，中文文档，不存在语言障碍，易于理解和学习；
    3. 双向数据绑定：保留了angular的特点，在数据操作方面更为简单；
    4. 组件化：保留了react的优点，实现了htlm的封装和重用，在构建单页面应用方面有着独特的优势；
    5. 视图、数据、结构分离：使数据的更改更为简单，不需要进行逻辑代码的修改，只需要操作数据就能完成相关操作；
    6. 虚拟DOM，dom操作是非常耗费性能的，不再使用原声的dom操作节点，极大解放了dom操作，但是还是会具体操作dom，只是换了一种方式；
    7. 运行速度更快，相比较于react而言，同样是操作虚拟dom，就性能而言，vue存在很大的优势；
###2. 父组件向子组件传递数据；
    通过props
###3. 子组件向父组件传递事件
    1. 父组件中把方法作为属性传入子组件中，在子组件中调用父组件的方法；
    2. 先在父组件中监听某个事件、然后在子组件中通过emits获取，并通过$emit('event')触发这个事件；
    3. 在子组件中直接通过this.$parent.event调用父组件的方法；
###4. v-show和v-if指令
    共同点：都能够控制元素的显示与隐藏；
    不同点：实现的原理不同，v-show的本质是通过控制css的display设置为none，来实现隐藏或显示的目的，整个过程中，DOM是一直存在的；
          而v-if在编译过程中会被转化成三元表达式，即当条件不满足时，DOM树中不会渲染该节点，
          使用v-if相当于动态地向DOM树中添加或者删除DOM元素，因此需要不停地销毁和创建DOM，更加消耗性能，
    总结：如果需要频繁切换某个节点，优先使用v-show;
    
    拓展补充：display: none、visibility: hidden、opacity: 0的区别
        1. 是否占据DOM位置：
            display：none隐藏之后不会占据相当于在DOM树移除了，不会占据空间，
            visibili：hidden和opacity：0依旧会占据空间；
        2. 子元素是否继承：
            display：none： 不会被继承，但是由于父元素已经不在DOM树中了，因此就算不会继承该属性，子元素也不会显示出来；
            visibility：hidden：会被继承，可以通过设置子元素visibility: visible来显示子元素；
            opacity: 0: 会被子元素继承，但是不能设置子元素opacity：0来重新显示子元素；
        3. 事件绑定： 
            display: none： 元素已经从DOM树中移除了，因此自然是无法触发绑定的事件；
            visibility: hidden： 不会触发绑定的事件；
            opacitiy：0： 元素绑定的事件是可以被触发的；
        4. 过渡事件：
            transition对display和visibility是无效的；
            transition对opacity是有效的；
        简要记法：
            display：none是将元素从DOM树中移除掉了；
            visibility：hidden相相当于将元素整个替换成了空白的容器，也没有事件绑定；
            opacity：0相当于将元素的颜色设置为了透明，其余事件绑定都还存在；
###6. 如何让css只在当前组件中起作用？
    在组件的style标签中加上scoped
###7. <keep-alive></keep-alive>的作用是什么
    keep-alive是Vue内置的一个组件，可以使被包含的组件保留状态，避免重复渲染；
###8. 如何获取dom
    通过ref='domName'，用法：this.$refs.domName
###9. Vue当中的指令和用法：
    1. v-text: 
        更新元素的文本内容（textContent），<span v-test="msg"></span>等价于<span>{{ msg }}</span>;
    2. v-html: 
        赋值给元素的innerHTML，内容将会按照普通HTML插入，不会作为Vue模版进行编译，且scoped不会应用在v-html内部；
        注意XSS攻击；
    3. v-show: 
        控制元素的展示或者隐藏，原理是修改元素的css display属性；
    4. v-if/v-else/v-else-if: 
        控制元素的展示或者隐藏，原理是操作DOM（添加或者删除），在render函数中就是一个三元表达式；
    7. v-for: 
        基于源数据遍历渲染元素或模版块；
    8. v-on: 
        绑定事件监听器，事件类型由参数指定，并且可以指定修饰符、以及绑定多个监听器；
    9. v-bind: 
        动态绑定元素的属性，或者组件的prop；
    10. v-model: 
        在表单控件或组件上创建双向绑定；
    11. v-slot: 
        插槽
    12. v-pre: 
        跳过这个元素以其子元素的编译过程，元素的内容将会被直接渲染出来，跳过大量没有指令的节点会加快编译。；
    13. v-cloak:
        这个指令会保持在元素上，直到关联组件实例结束编译，一般用于防止页面加载时出现 vuejs 的变量名；
        v-cloak指令可以解决初始化慢而导致页面闪动的一个方案，如果是在有工程化的项目里面，
        项目的HTML结构中就只有一个空的DIV元素，其他的都是让路由去挂载不同组件来完成的，就不需要v-cloak指令的了
    14. v-once: 
        只会渲染元素或者组件一次；
        在此后的重新渲染(update)过程中，元素以及它们的子元素，将会被视作静态内容并跳过，这可以优化组件更新时的性能；
        注意：如果v-once绑定vuex全局状态，则页面刷新后元素消失；
    15. v-is: vue 3.x中被废弃，需要使用is属性代替；
###10. v-for为什么要使用key
    key可以来为每一个节点做一个唯一标识，这样Diff算法就可以正确识别这个DOM，作用是为了更高效地更新虚拟DOM
###11. v-model的使用
    v-model通常用于表单数据的双向绑定，实际上它的本质是一个语法糖，背后就做了两个操作：
    1. v-bind绑定一个value属性；
    2. v-on绑定一个input事件；
###11. 简述computed、watchEffect和watch的使用场景：
    computed: 
        computed是计算属性，通过依赖于其他属性来计算值，并且computed的值具有缓存，只有当计算值变化时才会返回内容；
        当多条数据影响一条数据的时候使用；
        PS: computed可以设置getter和setter
    watchEffect：
        响应式地监听副作用的依赖项；
        当依赖项发生改变时，重新执行副作用；
    watch: 
        可以侦听特定的数据源，当数据源发生改变时，在单独的回调函数中执行副作用，
        当一条数据影响多条数据时使用；
        
    watch 与 watchEffect 的比较，watch 允许我们：
        1、惰性地执行副作用；
        2、更具体地说明应触发侦听器重新运行的状态；
        3、访问被侦听状态的先前值和当前值。
    watch 与 watchEffect 在手动停止，副作用无效 (将 onInvalidate 作为第三个参数传递给回调)，flush timing 和 debugging 方面有相同的行为。
###12 watch和watchEffect的区别：
    watch 是需要传入侦听的数据源，而 watchEffect 是自动收集数据源作为依赖。
    watch 可以访问侦听状态变化前后的值，而 watchEffect 没有，watchEffect获取的改变后的值。
    watch 是属性改变的时候执行，当然也可以immediate，而 watchEffect 是默认会执行一次(相当于自带 immediate)，然后属性改变也会执行。
###11. v-on可以监听多个事件吗
    可以，例如：<input v-on="{click: onClick, focus: onFocus}" />
###11. $nextTick的使用；
    将回调推迟到下一个 DOM 更新周期之后执行。在更改了一些数据以等待 DOM 更新后立即使用它。
    Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中，原因是在created()钩子函数执行的时候DOM 其实并未进行任何渲染，而此时进行DOM操作无异于徒劳，所以此处一定要将DOM操作的js代码放进Vue.nextTick()的回调函数中。与之对应的就是mounted钩子函数，因为该钩子函数执行时所有的DOM挂载已完成。
###11. Vue中的data为什么是一个函数
    组件中的data写成一个函数，这样数据以函数返回值的形式定义，每次复用组件的时候，都会返回一份新的data；
    相当于每个组件实例都有自己私有的数据空间，每个组件都只负责维护各自的数据，不会造成混乱，
    如果将写成对象形式，那么所有的组件实例共用了一个data，这样改一个全部都发生改变了；
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

###11. Vue中双向数据绑定是如何实现的
    vue双向数据绑定是通过数据劫持，结合发布订阅模式的方式来实现的（数据劫持 + 观察者模式）；
    也就是说数据和试图同步，数据发生改变，试图跟着变化，试图变化，数据也跟着发生改变
    原理：
        对象内部通过defineReactive方法，使用Object.defineProperty将属性进行劫持（只会劫持已存在的属性）；
        数组则是通过重写数据来实现的，当页面使用对应属性时，每个属性都拥有自己的dep属性，存在他所依赖的watcher（依赖收集）get，
        当属性变化后会通知自己对应的wacher去更新（派发更新）set；
        1. Object.defineProperty数据劫持
        2. 使用getter收集依赖，setter通知watcher派发更新
        3.watcher发布订阅模式；
       
    核心：关于Vue双向数据绑定，其核心是Object.defineProperty()方法
###11. 单页面应用和多页面应用的区别及优缺点
    单页应用SPA，指只有一个主页面的应用，浏览器一开始要加载所有必须的html,js,css。所有的页面内容
    都包含在这个所谓的主页面中，但在写的时候，还是会分开写页面片段，然后在交互的时候由路由程序动态载入，
    单页面的页面跳转，仅刷新局部资源，多应用与pc端；
    多页应用MPA，就是指在一个应用里面有多个页面，页面跳转的时候是整页刷新；
    
    单页应用优点：响应速度快，内容的改变不需要重新加载整个页面，因此对服务器的压力小；
    前后端分离，页面效果可能会比较炫酷（比如切换页面内容时候的转场特效）
    
    单页应用缺点：不利于SEO，导航不可用，如果一定要导航需要自行实现前进后退。
    （由于单页应用不能用浏览器的前进后退功能，所以需要自己建立堆栈管理），初次加载时耗时多，页面复杂度提高很多；
###11. v-if和v-for的优先级
    当v-if和v-for一起使用时，v-for具有比v-if更高的优先级；
    这意味着v-if将分别重复运行于每一个v-for循环中，不推荐两者同时使用（或将v-if放在外层）；
###12. assets和static的区别
    assets中的静态文件会被打包压缩进入index.html文件中；
    static中的资源文件不会经过打包压缩，而是直接上传到服务器；
###13. vue常用修饰符
    .stop: 相当于event.stopPropagation();
    .prevent：相当于event.preventDefault；
    .capture：与事件冒泡的方向相反，事件捕获由外到内；
    .self：只会触发自己范围内的事件，不包含子元素；
    .once：只会触发一次
###14. Vue的两个核心点
    数据驱动：Viewmodel，保证数据和视图的一致性；
    组件系统：应用类UI可以看做全部是由组件树构成的；
###15. Vue和Jquery的区别
    jquery是使用选择器选取DOM对象，对其进行赋值、取值、事件绑定等操作，其实和通过原生的js操作html的区别只是在于
    可以更加方便的选取和操作DOM对象，而数据和界面是在一起的：$("lable").val()，比如需要获取label标签的内容，那么它还是依赖于DOM元素的值；
    Vue则是通过Vue对象将数据和View完全分离开来了，对数据进行操作不再需要引用相应的DOM对象，可以说数据和视图是分离的；
    数据和视图通过Vue对象这个vm实现相互的绑定，这就是MVVM框架的定义；
###16. SPA首屏加载慢的解决方法
    使用懒加载所需的资源，优化CDN分发；
###17. Vue-router跳转和location.href有什么区别
    使用location.href来跳转简单方便，但是刷新了页面；
    使用history.pushState('/url')，无刷新页面，静态跳转；
    引进router，使用router.push('/url')，使用了diff算法，实现了按需加载，减少了dom的消耗；
    其实使用router跳转和使用history.push跳转没有太多区别；'
###18. 讲一下vue slot
    简单来说，假如父组件需要在子组件中放入一些DOM，那么这个DOM是否显示、在哪儿显示、如何显示，就是由slot分发负责；
###19. axios的特点有哪些
    从浏览器中创建XMLHttpRequests；
    node.js创建http请求；
    支持promise API；
    拦截请求和响应；
    转换请求数据和响应数据；
    取消请求；
    自动转换成JSON
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
    使用vue开发时，在vue初始化之前，由于div是不归vue管的，所以我们写的代码在还没有解析的情况下
    会很容易出现花屏现象，看到类似于{{message}}的字样，可以在css里面加上[v-cloak]： {dispaly: none}
    如果没有彻底解决，则在跟元素加上style="display: none;" :style="{display: 'block'}"
###23. Vue常用组件库
    Element，Mint UI， VUX；
###24. 什么是vue生命周期？有什么作用；
    每个Vue实例在被创建时都要经过一系列的初始化过程-例如，需要设置数据监听、编译模版、将实例挂载到DOM并在数据变化时候更新DOM等；
    同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会；
    （ps：生命周期钩子就是生命周期函数），例如如果要通过某些插件操作DOM节点，如想在页面渲染完成后弹出广告窗，那么我们就可以在在mounted中进行；
###25. 第一次页面加载会触发哪几个钩子；
    beforeCreate， createed, beforeMount, mounted;
###26. Vue生命周期
    beforeCreate: 
        在实例初始化之后、数据观测和事件配置之前被调用；
        在这一阶段，data、methods、computed以及watch中的数据都还没有初始化，
        不能在这个阶段使用data中的数据和methods中的方法；
    create：
        在实例已经创建完成之后调用；
        在这一阶段中，实例已经完成了数据观测和事件配置；
        data和methods都已经被初始化好了，可以操作data中的数据，或者调用methods中的方法；以及绑定computed、watch等；
        网络请求最早可以在这个阶段中进行；
        注意：此时还没有$el，如果要想和DOM进行交互，可以通过vm.$nextTick来访问DOM；
    beforeMounted: 
        在组件被挂载之前调用；
        执行到这个钩子的时候，在内存中已经编译好了模版了，但是还没有挂载到页面中，此时，页面还是旧的；
    mounted: 
        在组件被挂载之后被调用；
        在这一阶段，真实的DOM挂载完成，数据完成双向绑定，可以访问DOM节点，
        如果我们想要通过副作用操作页面中的DOM节点，最早可以在这个阶段进行；
    beforeUpdate: 
        当数据更新时调用；
        发生在虚拟DOM重新渲染和打补丁（patch）之前，也就是说，当执行这个钩子时，
        页面显示的数据还是旧的，而data中的数据是更新后的，页面还没有和最新的数据保持同步；
        可以在这个钩子中进一步更改状态，这不会触发附加的重渲染过程
    updated: 
        数据更新完成后调用；
        页面显示的数据和data中的数据已经保持同步了，都是最新的；
        这一期间应当避免再次更新数据，因为这样可能导致无限循环的更新；
    beforeDestory:
        组件实例被销毁之前调用；
        这一阶段所有的data和methods，指令，过滤器，都是处于可用状态，还没有真正被销毁；
        可以在这个时候清除定时器等；
    destoryed: 
        组件实例销毁之后调用，
        调用后，Vue实例指示的东西都会被解除绑定，所有事件监听器都会被移除；
        这个时候所有的data, methods, 指令，过滤器等都是不可用状态；
    activated:
        keep-alive专属，组件被激活的时候调用；
    deactivated:
        keep-alive专属，组件被销毁时调用；
###27. create和mounted的区别
    create： 在模版渲染成html前调用，即通常初始化某些属性值，然后再渲染成视图；
    mounted：在模版渲染成为html后调用，通常是初始化页面完成后，再对html的dom节点进行一些需要的操作；
###28. vue异步请求一般是在哪个周期函数；
    可以在createed/beforeMounted/mounted中进行异步请求；
    因为在这三个钩子函数中，data已经创建，可以将服务端返回的数据保存在data中；
    ps：如果异步请求不需要依赖DOM，推荐在created钩子函数中进行异步请求，优点如下：
            1. 能够更快获取到服务端数据，减少页面loading时间；
            2. ssr不支持beforeMount， mounted钩子函数，放在created中有助于一致性；
        但是如果要操作DOM，那么肯定是在mounted的时候进行；
###29. 请详细说下你对Vue生命周期的理解；
    总共分为8个阶段： 创建前/后，挂载前/后，更新前/后，销毁前/后；
    。。。
###30. mvvm框架是什么
    vue是实现了双向数据绑定的mvvm框架，当视图View改变时更新模型层，当模型层改变的时候更新视图层；
###31. vue-router是什么，它有哪些组件
    vue-router是一个用来写路由的库，包括router-link、router-view等组件；
###32. $route 和 $router的区别
    $router是VueRouter的实例，在script标签中想要导航到不同的URL，使用$router.push方法
    $route是当前的router跳转对象，里面可以获取当前路由的name, path, query, params等；
###33. vue-router的两种模式
    1. hash模式：即地址栏的#符号
    2. history模式: window.history对象
###34. vue-router实现路由懒加载
###35. vuex是什么？哪种功能场景使用它
    vuex是一个vue的状态管理库，用于管理全局状态；
###36. vuex有哪几种属性
    有5种，分别是state, getter, mutation, action, module
    state: 基本数据（数据源存放地）
    getter: 从基本数据中派生出来的数据
    mutation: 提交更改数据的方法，同步
    action: 异步下更改数据的方法，调用mutations
    module: 模块化vuex
# https://www.cnblogs.com/wenshaochang123/p/14888494.html
###37. MVC和MVVM的区别
###38. MVC和MVVM的区别
    1. MVC全名model-View-Controller(模型-视图-控制器)，一种软件设计典范；
        model: 是用于处理应用程序数据逻辑部分，通常模型对象负责在数据库中存取数据；
        View: 是应用程序中处理数据显示的部分，通常视图是依据模型数据创建的；
        Controller: 是应用程序处理用户交互的部分，通常控制器负责从视图读取数据，控制用户输入，并想模型发送数据；
      MVC思想：一句话描述就是Controller负责将model的数据用View显示出来，换句话说就是Controller把model的数据赋值给View；
    2. MVVM新增了VM类（Viewmodel层），
        Viewmodel层：通过两件事做到了数据的双向绑定：
        一是将【模型】转化为【视图】，即将后端传递的数据转化成所看到的页面，实现的方式是：数据绑定；
        二是将【视图】转化为【模型】，即将所看到的页面转化成后端的数据，实现的方式是：DOM事件监听；
    3. MVC和MVVM的最大区别就是：实现了View与model的自动同步，也就是说当Model的属性发生的时候，我们不再需要手动地
        去操作DOM元素来改变View的显示，二是改变属性后该属性对应的View层显示会自动改变（对应Vue数据驱动的思想）
        整体来看，MVVM比MVC精简了许多，不仅简化了业务与界面的依赖，还解决了数据频繁更新的问题，不用再用选择器来操作DOM元素；
        因为在MVVM中，View不知道Model的存在，Model和ViewModel也察觉不到View，这种低耦合模式提高了代码的可重用性；
        注意：Vue并没有完全遵循MVVM的思想；
###39. 为什么官方要说Vue没有完全遵循MVVM思想
    严格的MVVM要求View不能和Model直接通信，而Vue则提供了$refs这个属性，让Model可以直接操作View，这违背了MVVM的思想；

###38. vue组件通讯有哪些方式
        1. props和emit: 父组件向子组件传递数据是通过props传递的，子组件传递给父组件是通过$emit触发事件来做到的；
        2. $parent和$children：获取当前组件的父组件和当前组件的子组件；
        3. $attr和$listeners: 
        4. 父组件通过provide来提供变量，然后在子组件中通过inject来注入变量。（官方不推荐在实际业务中适用，但是写组件库时很常用。）
        5. $refs获取组件实例；
        6. eventBus兄弟组件数据传递，这种情况下可以使用事件总线的方式；
        7. vuex状态管理；
        8.     
###40. 如何理解Vue的单向数据流
    1. 数据总是从父组件传递到子组件，即子组件通过props选项接受父组件传递的状态；
    2. 子组件没有权利修改父组件传过来的数据，只能请求父组件对原始数据进行修改，子组件通过$emit触发父组件方法，从而修改父组件的状态；
    这样可以防止因子组件意外改变父组件的状态，而导致你的应用数据流向难以理解；
    
    注意：在子组件中直接使用v-modal绑定父组件传过来的props是不规范的写法，开发情况会报警告；

###41. v-if和v-for为什么不建议一起使用
    v-if 和 v-for 不能在同一标签中使用，v-for具有比v-if更高的优先级，这意味着v-if会运行在每一个v-for循环中；
###42. vue如何检测数组变化
    数组考虑性能原因没有用 defineProperty 对数组的每一项进行拦截，而是选择对7种数组（push,shift,pop,splice,unshift,sort,reverse）方法进行重写（AOP 切片思想）。
    
    所以在 Vue 中修改数组的索引和长度无法监控到。需要通过以上7种变异方法修改数组才会触发数组对应的watcher进行更新。   
###43. vue3.0了解过吗
    1. 响应式原理的改变：Vue3.x使用Proxy取代Vue2.x版本的Object.defineProperty;
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
    4. 父beforeDestroy -> 子beforeDestroy -> 子destroyed -> 父destroyed
###46. 虚拟DOM是什么，有什么优缺点
    由于在浏览器中操作DOM是非常昂贵的，频繁操作DOM，会产生一定的
    

    





