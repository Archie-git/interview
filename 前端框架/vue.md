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
###7. <keep-alive></keep-alive>的作用是什么？
    keep-alive是Vue内置的一个组件，可以使被包含的组件保留状态，避免重复渲染；
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
    watch 是需要传入侦听的数据源，而 watchEffect 是自动收集数据源作为依赖。
    watch 可以访问侦听状态变化前后的值，而 watchEffect 没有，watchEffect获取的改变后的值。
    watch 是属性改变的时候执行，而 watchEffect 是默认至少会执行一次。
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
    使用vue开发时，在vue初始化之前，由于div是不归vue管的，所以我们写的代码在还没有解析的情况下
    会很容易出现花屏现象，看到类似于{{message}}的字样，可以在css里面加上[v-cloak]： {dispaly: none}
    如果没有彻底解决，则在跟元素加上style="display: none;" :style="{display: 'block'}"
###23. Vue常用组件库
    Element，Mint UI， VUX；
###24. 什么是vue生命周期？有什么作用；
    view实例从创建到销毁的过程，就是生命周期，从开始创建、初始化数据、编译模版、挂载DOM->渲染、更新->渲染、销毁等一系列过程，称之为Vue的生命周期；
    
    每个Vue实例在被创建时都要经过一系列的初始化过程-例如，需要设置数据监听、编译模版、将实例挂载到DOM并在数据变化时候更新DOM等；
    同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会；
    （ps：生命周期钩子就是生命周期函数），例如如果要通过某些插件操作DOM节点，如想在页面渲染完成后弹出广告窗，那么我们就可以在在mounted中进行；

###25. 第一次页面加载会触发哪几个钩子；
    beforeCreate， createed, beforeMount, mounted;
###26. Vue生命周期
    beforeCreate: 
        在数据观测和事件配置之前被调用；
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
        （编译模版：利用data中的数据和模版生成html文档，注意此时html还未挂载到页面上）
    mounted: 
        在组件被挂载之后被调用（el被新创建的vm.$el替换）；
        在这一阶段，真实的DOM挂载完成，数据完成双向绑定，可以访问DOM节点，
        如果我们想要通过副作用操作页面中的DOM节点，最早可以在这个阶段进行；
        （这一阶段将会利用上面编译好的html内容替换el属性指向的DOM对象，渲染到页面上）
    beforeUpdate: 
        当数据更新时调用；
        发生在虚拟DOM重新渲染和打补丁（patch）之前，也就是说，当执行这个钩子时，
        页面显示的数据还是旧的，而data中的数据是更新后的，页面还没有和最新的数据保持同步；
        可以在这个钩子中进一步更改状态，这不会触发附加的重渲染过程
    updated: 
        由于数据更新导致虚拟DOM重新渲染完成后调用；
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
    由于在浏览器中操作DOM是非常昂贵的，频繁操作DOM，会产生一定的性能问题，这就是虚拟DOM的产生原因；
    虚拟DOM的本质就是用一个原生的JS对象去描述一个DOM节点，是对真实DOM的一层抽象；
    
    优点：
        1. 保证性能下限：框架的虚拟DOM需要适配任何上层API可能产生的操作，它的一些DOM操作的实现必须是普适的，所以它的性能不是最优的；
           但是比起粗暴的DOM操作性能要好很多，因此框架的虚拟DOM至少可以保证你在不需要手动优化的情况下，还能拥有不错的性能，即保证性能下限；
        2. 无需手动操作DOM：我们只需要写好View-Model层的代码逻辑，框架会根据虚拟DOM和双向数据绑定，帮助我们以可预期的方式更新视图，极大地提高我们的开发效率；
        3. 跨平台，虚拟DOM的本质是javascript对象，而real DOM与平台强相关，相比之下虚拟DOM可以更加便捷地进行跨平台操作，比如服务端渲染，weex开发等；
    
    缺点：
        1. 首次渲染大量DOM的时候，由于多了一层DOM计算，会比innerHTML插入慢；       
###47. v-modal的原理
    v-modal本质上是一个语法糖（指在现有js语言语法和功能的基础上，增加了一些代码逻辑和使用规则，从而更方便程序员使用。）    
    
    v-modal在内部为不同的输入元素使用不同的property并抛出不同的事件；
        1. text和textarea元素使用value property和input事件；     
        2. checkbox和redio使用chcked property和change事件；
        3. select字段将value作为prop并将change作为事件；

###48. Vue事件绑定原理
    原生事件绑定是通过addEventListener绑定给真实元素的，组件事件绑定是通过Vue自定义的v-on实现的；
    如果要在组件上使用原生事件，需要加上.native修饰符，这样就相当于在父组件中将子组件当作普通的html标签，然后加上原生事件；
    
    on、emit是基于发布订阅模式的1，维护一个事件中心，on的时候将事件按照名称保存在事件中心里，称之为订阅者；
    然后通过emit将对应的事件进行发布，去执行事件中心里对应的监听器；

###49. vue-router路由钩子函数是什么？执行顺序是什么？
    钩子函数的种类有：全局守卫、路由守卫、组件守卫；
    
    完整的导航解析流程：
        1. 导航被触发。
        2. 在失活的组件调用beforeRouterUpdate
        2.
        2.
        2.
        2.
        2.
        2.
        2.
        2.
        2.
###50. vue-router动态路由
###51. 谈一下对vuex的理解
    vuex是专门为vue提供的全局状态管理系统，用于多个组件中共享数据、数据缓存等（无法持久化存储，内部原理是通过创造一个全局实例new Vue）；
    主要包括以下几个模块：
        State：定义了应用状态的数据结构，可以在这里设置默默人的初始化状态；
        Getter：允许组件从Store中获取数据，mapGetters辅助函数的作用仅仅是将store中的getter映射到局部计算属性；
        Mutation：是唯一更改store的方法，必须是同步函数，store.commit；
        Action：用于提交mutation，而不是直接变更状态，可以包含任意异步请求, store.dispath；
        Module：允许将单一的Store拆分更多个store且保存在单一的状态树中；
###52. Vuex页面刷新数据丢失怎么解决
    需要做vuex数据持久化，一般使用本地存储的方案来保存数据（cookie，localStorage，sessionStorage，indexDB等）
###53. Vuex为什么要分模块并且加命名空间；
###54. 使用过SSR吗
    SSR也就是服务端渲染，也就是将React，Vue在客户端把标签渲染成HTML的工作放在服务端完成，然后把html直接返回给客户端
    优点：SSR有着更好的SEO，并且首屏加载速度更快
    缺点：服务端渲染应用程序需要处于node.js运行环境，并且会让服务器有更大的负载需求；
###55. vue中使用了哪些设计模式
    工厂模式：传入参数即可以创建实例，虚拟dom根据参数的不容返回基础标签的Vnode和组件Vnode；
    单例模式：整个程序有且仅有一个实例；   
    发布订阅模式：vue事件机制
    观察者模式：响应数据原理
    装饰器模式
    策略模式
###56. Vue性能优化
    对象层级不要过深，否则性能很差
    不需要响应式的数据不要放在data中，可以使用Object.freeze()冻结数据；
    v-if和v-show区分使用场景
    computed和watch区分场景使用
    v-for必须加上key，并且v-for中避免使用v-if
    大数据列表和表格性能优化：虚拟列表 / 虚拟表格
    防止内部泄漏，组件销毁前将全局变量和定时器销毁；
    图片懒加载
    路由懒加载
    异步路由
    第三方插件按需加载
    适当采用keep-alive缓存组件
    防抖节流的运用
    服务端SSR或者预渲染
###57 vue.mixin的使用场景和原理
###58 nextTick的使用场景和原理
    nextTick中的回调是在下次DOM更新循环结束之后执行的延迟回调，在修改数据之后立即调用这个方法，获取更新后的DOM；
    主要思路就是采用微任务优先的方式调用异步方法去执行nextTick包装的方法；
###59. keep-alive的使用场景和原理；
    keep-alive是Vue内置的一个组件，可以实现组件缓存，当组件切换时不会对当前组件进行卸载；
    常用的两个属性include/exclude，允许有条件的进行缓存；
    两个生命周期activated/deactivated，用来得知当前组件是否处于活跃状态。
    keep-alive运用了LRU算法，选择最近最久未使用的组件予以淘汰：
        1. 将新数据从尾部插入到this.keys中，
        2. 每当缓存命中（即缓存数据被访问），则将数据移动到this.keys的尾部
        3. 当this.keyss满的时候，将头部的数据丢弃
###60. 有写过自定义指令吗，原理是什么
    指令本质上是装饰器，是vue对HTML元素的拓展，给HTML元素添加自定义功能，vue编译DOM的时候，会找到指令对象，执行指令的相关方法；
    
    自定义指令有5个生命周期（也叫钩子函数），分别是bind, inserted, update, componentUpudated, unbind
        1. bind: 只调用一次，指令第一次绑定到元素时调用，在这里可以进行一次的初始化设置；
        2. inserted：被绑定的元素插入父节点时调用；
        3. update：被绑定元素所在的模版更新时调用，而不论绑定值是否变化，通过比较前后的绑定值；
        4. unbind：只调用一次，指令与元素解除绑定的时候调用；
    
    原理：
        1. 在生成ast语法树的时候，遇到指令会给当前元素添加directives属性
        2. 通过genDirectives生成指令代码
        3. 在patch前将指令的钩子提取到cbs中，在patch过程中调用对应的钩子；
        4. 当执行指令对应的钩子函数时，调用对应指令的自定义方法
        
###61. vue修饰符有哪些
    事件修饰符
        .stop：阻止事件继续传播
        .prevent：阻止标签默认行为
        .capture：只用事件捕获模式，即元素自身触发的事件现在此处理，然后再交由内部元素进行处理
        .self：只当在event.targe是当前元素自生是触发该函数
        .once：事件只会触发一次
        .passive：告诉浏览器你不想阻止事件的默认行为
    v-modal修饰符
        .lazy：通过这个修饰符，转变为chang事件再同步；
        .number：自动将用户输入值转化为数值类型；
        .trim：自动过滤用户输入的收尾空格；
    键盘事件修饰符
        .enter
        .tab
        .delete
        .esc
        .space
        .up
        .down
        .left
        .right
    系统修饰符
        .ctrl
        .alt
        .shift
        .meta
    鼠标按钮修饰符
        .left
        .right
        .middle
###62. Vue模版编译原理
    Vue的编译过程就是将template转化成render函数的过程，分为以下三步：
        1. 第一步将模版字符串转化成element ASTs(解析器)
        2. 第二步是对AST进行静态节点标记，主要用来做虚拟DOM的渲染优化（优化器）
        3. 第三步是使用element AST生成render函数代码字符串（代码生成器）
###63. 生命钩子是如何实现的
    Vue的生命周期钩子核心实现是利用发布订阅模式先把用户传入的生命周期钩子订阅好（内部采用数组的方法存储）；
    然后在创建组件实例的过程中会一次执行对应的钩子方法（发布）；
###64. vue-router中常见的路由模式和实现原理
    hash模式：
        1. location.has的值实际就是url中#后面的东西，
            它的特点在于：hash虽然出现于URL中，但不会被包含在HTTP请求中，对后端完全没有影响，因此改变hash不会重新加载页面；
        2. 可以为hash的改变添加监听事件
            window.addEventListener("hashchange", funcRef, false)；
            每一次改变hash，都会在浏览器的访问历史中增加一个记录，利用hash的以上特点；
            就可以实现前端路由"更新水土但不重新请求页面"的功能了；
        特点：兼容性好，但是不美观；
    history模式： 
        利用了HTML History Interface中新增的pushState() 和 replaceState方法()
        这两个方法应用于浏览器的历史记录栈，在当前已有的back，forward，go的基础上，它们提供了对历史记录进行修改的功能；
        
        这两个方法有一个共同点：当调用他们修改浏览器历史记录栈后，虽然当前URL改变了，但浏览器不会刷新页面，
            这就为单页面应用前端路由"更新视图但不更重新请求页面"提供了基础
###65. diff算法
    diff算法采用同级比较
        1. tag标签不一致直接新节点替换旧节点；
        2. tag标签一样：先替换属性，对比子元素
        3.       
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
### 78. vue的路由拦截器的作用
    例如：权限设置，当用户没有登录权限的时候就会跳转到登录页面，用到的字段requireAuth:true

### 79. vue生命周期总共有几个阶段
    8个：创建前/后、载入前/后、更新前/后、销毁前/后；
    
### 80. vuex路由钩子函数
    首页可以控制导航跳转，beforeEach， afterEach等，一般用于页面title的修改，一些需要登录才能调整页面的重定向功能；
    beforeEach： 主要有三个参数：to, from, next
    to: route即将进入的目标路由对象
    from：route当前导航正要离开的路由
    next：function一定要调用该方法resolve这个钩子，执行效果依赖next方法的调用参数，可以控制网页的跳转；
### 81. vue如何自定义一个过滤器；
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
### 85. 如何给vue自定义组件添加点击事件
    需要在@click后面添加.native，官方对于native的解释为：监听组件根元素的原生事件        
### 86. 绑定class的数组用法
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

### 92. vue事件如何使用event对象
    <button v-on:click="Event($event)">chick</button>
    
### 93. 完整的 vue-router 导航解析流程
    1.导航被触发；
    2.在失活的组件里调用beforeRouteLeave守卫；
    3.调用全局beforeEach守卫；
    4.在复用组件里调用beforeRouteUpdate守卫；
    5.调用路由配置里的beforeEnter守卫；
    6.解析异步路由组件；
    7.在被激活的组件里调用beforeRouteEnter守卫；
    8.调用全局beforeResolve守卫；
    9.导航被确认；
    10..调用全局的afterEach钩子；
    11.DOM更新；
    12.用创建好的实例调用beforeRouteEnter守卫中传给next的回调函数。
### 94 is的用法
### 95 vue更新数组时触发视图更新的方法
### 96 解决非工程化项目初始化页面闪动问题

### 以下todo
vue-router
1、vue-router如何响应 路由参数 的变化？
2、完整的 vue-router 导航解析流程
3、vue-router有哪几种导航钩子（ 导航守卫 ）？
4、vue-router传递参数的几种方式
5、vue-router的动态路由匹配
6、vue-router如何定义嵌套路由？
7、<router-link></router-link>组件及其属性
8、vue-router实现路由懒加载（ 动态加载路由 ）
9、vue-router路由的两种模式
10、history路由模式配置及后台配置











