### https://blog.csdn.net/eyeofangel/article/details/88797314
### https://blog.csdn.net/MichelleZhai/article/details/118423494
### hooks：https://blog.csdn.net/MichelleZhai/article/details/118392437

### hooks: https://blog.csdn.net/kellywong/article/details/106430977
### https://www.php.cn/js-tutorial-457313.html

#React基础
#Redux相关
#React Router相关

#React基础
###1. RealDOM和VirtualDOM的区别
    1. RealDOM更新缓慢、VirtualDOM更新迅速；
    2. RealDOM可以直接更新HTML，Virtual无法直接更新HTML；
    3. RealDOm中如果元素更新，则会创建新的DOM，VirtualDOM中如果元素更新，则会更新JSX；
    4. RealDOM的DOM操作代价很高，VirtualDOM的DOM操作代价较低；
    5. RealDOM消耗内存多，VirtualDOM消耗内存少；
###3. React的特点
    高性能虚拟DOM：React通过实现虚拟DOM，并配合diff算法，最大限度地减少与真实DOM的交互，从而提升性能；
    组件化开发：通过 React 构建组件，使得代码更加容易得到复用，能够高效率的应用在大项目的开发中；
    数据驱动：所谓数据驱动就是指开发者不需要直接操作DOM，当数据发生了变化，DOM会跟着变化，而视图可以通过设置事件监听来更新数据；
    单向数据流：React中的数据是单向自顶向下传递的，数据可以从父组件传递到子组件，而子组件只能通过调用父组件的方法，来通知父组件修改自身的数据；
    JSX扩展：是一个JavaScript的语法扩展，使用JSX可以简化组件化开发的渲染逻辑，增强代码可读性；
###4. React的主要优点
    简洁：采用声明式和数据驱动的模式，无需手动操作DOM；
    灵活：使用组件化开发的模式，增强了代码的可复用性；
    高效：虚拟DOM使得页面渲染速度更快；
###6. 为什么浏览器无法读取JSX
    浏览器只能理解原始的Javascript语法，而不能读取常规Javascript对象中的JSX；
    所以，为了使浏览器能够理解JSX，需要先用像Babel这样的JSX转换器将JSX语法转换成原始Javascript语法；
###7. 如何理解，在React中，一切都是组件这句话
    1.组件是UI视图的基础构件，整个UI视图可以看作是由多个小的组件构成的；
    2.每个组件都相互独立并且可重用，修改某一个组件的实例属性，不会影响同一组件的其他实例；
###12. React组件生命周期方法
    图表：https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

    React生命周期执行过程包括挂载、更新和卸载三个阶段：
    1.挂载阶段（这个是组件从创建到挂在到DOM上的阶段）
        constructor(props)：
            在React组件挂载之前，会调用它的构造函数。
            通常，在React中，构造函数仅用于以下两种情况：初始化内部state，绑定事件处理函数；

        static getDerivedStatefromProps(props, state)：
            该方法会在组件挂载阶段及后续更新阶段被调用；
            它应返回一个对象来更新state，如果返回null则不更新任何内容；
            适用场景：state的值在任何时候都取决于props；
                
            注意：派生状态会导致代码冗余，并使组件难以维护，不建议使用；

        render():
            render函数是一个纯函数，表示将组件渲染到页面上；

        componentDidMount()：
            会在组件挂载后（插入DOM树后）立即调用；
            可以在这一阶段通过网络请求获取数据，以及添加订阅（需要在componentWillUnmount() 里取消）等；

    2.更新阶段（组件被挂载到DOM之后，当prop或者state发生改变时，或者直接调用forceUpdate()方法，会引起更新和重新渲染）：
        static getDerivedStatefromProps(props, state)：同上；

        shouldComponentUpdate(nextProps, nextState)：
            返回一个布尔值，判断当前state或props更改的变化，是否需要出发组件更新，此方法仅作为性能优化的方式而存在。
            注意：返回 false 并不会阻止子组件在state更改时重新渲染。

        render()：同上；

        getSnapShotBeforeUpdate：
            在更新阶段执行渲染之前调用，它使得组件能在发生更改之前从DOM中捕获一些信息（例如，滚动位置）。
            其任何返回值为snapshot的值（或 null），并且这个返回值参数传递给 componentDidUpdate()。 
            用法并不常见，但它可能出现在 UI 处理中，如需要以特殊方式处理滚动位置的聊天线程等。

        componentDidUpdate(prevProps, prevState, snapShot)：
            会在组件更新后会被立即调用，可以在此处对DOM进行操作。
            尽量避免在这一阶段setState，万不得已的情况下必须包裹在一个条件语句里；
            如果组件实现了 getSnapshotBeforeUpdate() 生命周期（不常用），
            
    3.卸载阶段（组件被销毁）
        componentDidUnmount：会在组件卸载及销毁之前直接调用，可以在此方法中执行必要的清理操作（清除定时器、取消订阅等）；

###14. 说一下React refs
    概念：Refs允许我们访问DOM节点、或在render方法中创建的React元素；

    使用场景：
        需要管理焦点、选择文本或者媒体播放时；
        触发式动画；
        与第三方DOM库集成；
   
    使用方式：
        创建：React.createRef()；
        绑定：<div ref={this.divRef}></div>；
        访问：this.divRef.current.textContent = 'hello dogge'；

    默认情况下，你不能在函数组件上使用 ref 属性，因为它们没有实例；
    如果要引用函数组件的ref，你可以使用forwardRef转发，同时可以结合useImperativeHandle来自定义暴露给父组件的实例值；

    React也支持另一种设置refs的方式，称为“回调 refs”。它能助你更精细地控制何时 refs 被设置和解除。

###30 什么是高阶组件
###31 高阶组件可以做什么
###32 React中Key的重要性
    key用于识别唯一的VirtualDOM元素以及驱动UI的相应数据，它们通过回收DOM中当前所有的元素来帮助React优化渲染。
    这些key必须是唯一的数字或者字符串，React只是重新排序元素而不是重新渲染它们，这样可以提高应用程序的性能；

    key是React中用于追踪哪些列表中元素被修改、删除或者被添加的辅助标识。
    在diff算法中，key用来判断该元素节点是被移动过来的还是新创建的元素，减少不必要的元素重复渲染。
###33. MVC框架的主要问题是
    1. 对DOM操作的代价非常高
    2. 程序运行缓慢且效率低下
    3. 内存浪费严重
    4. 由于循环依赖性，组件模型需要围绕models和views进行创建；
###34. 什么是Flux
    Flux是一种强制单向数据流的架构模式，他控制派生数据，并使用具有所有数据权限的中心store实现多个组件之间的通信；
    整个应用中的数据更新必须只能在此处进行，Flux为应用提供稳定性并且减少运行时候的错误；
###35. Redux的三个原则
    1. 单一数据源：整个应用的状态存储在单个store中的对象/状态树里，单一状态树可以更容易地更随时间的变化，并调试或者检查应用程序
    2. 状态是只读的：改变状态的唯一方法就是去触发一个动作，动作时描述变化的普通js对象；
    3. 使用纯函数进行修改：为了指定状态树如何通过操作进行转换，需要使用纯函数；
###36. 你对单一事实来源有什么理解
    Redux使用Store将程序的整个状态存储在同一个地方，因此所有组件的状态都存储在Store中，
    并且他们从store本身接受更新，单一状态树可以更加容易地跟踪时间的变化，并调试或者检查程序；
###39. 列出Redux的组件
    Action： 这是一个用来描述发生了什么事情的对象
    Reducer：这是一个确定状态将如何变化的地方
    Store：整个程序的状态/对象树都保存在Store中
    View：只显示Store提供的数据；
###40. 解释Reducer的作用
###41. Store在Redux中的意义是什么
    Store 是一个 JavaScript 对象，它可以保存程序的状态，并提供一些方法来访问状态、调度操作和注册侦听器。
    应用程序的整个状态/对象树保存在单一存储中。因此，Redux 非常简单且是可预测的。
    我们可以将中间件传递到 store 来处理数据，并记录改变存储状态的各种操作。所有操作都通过 reducer 返回一个新状态。
###42. React的diff算法工作过程
    传统的diff算法通过循环递归遍历节点进行对比，其复杂度要达到O(n^3)，其中n是节点总数，效率十分低下；
    tree diff：
        对树的每一层遍历，如果组件不存在了则会直接销毁；
    component diff：
        1. 同一类型的组件：继续比较下去，是否需要比较取决于shouldComponentUpdate；
        2. 不同类型的组件：直接替换；
    element diff：
        同一类型组件里：继续比较下去
###43. React中的setState是同步还是异步
    setState本身不是异步的，在React的生命周期函数或者作用域下是异步，在原生的环境下是同步的；
###44. setState为什么在React生命周期中是异步的
    1. Reacg框架本身的性能机制所导致的，因为每次调用setState都会触发更新，异步操作是为了提高性能，
        将多个状态合并到一起更新，减少re-render调用；
    2. React会将多个setState的调用合并为一个来执行，也就是说，当执行setState的时候，state中的数据并不会立即更新；
    参考： https://www.cnblogs.com/makai/p/14238200.html
###45. React服务端渲染
    目的：
        为了减少首屏加载等待时间；
        有利于SEO

    过程：
        1. 服务端接收到客户端请求，得到当前req,url,path，将jsx作为模版引擎，然后在已有的路由表内查找对应的组件；
            拿到需要请求的数据
        2. 将数据作为props,conetxt或者store的形式传入组件
        3. 然后基于React内置的服务端渲染api， renderToString()或者renderToNodeStream()把组件渲染成为html字符串或stream流；
        4. 再把最终的html进行输入钱需要将数据注入到浏览器，server输出（response后浏览器可以得到数据）
        5. 浏览器开始进行渲染和节点对比，然后执行组件的componnetDidMount完成组件内的事件绑定和一些交互；
        6. 浏览器重用了服务端输出的html节点，整个流程结束
        参考：https://juejin.cn/post/6844903943902855176

    这种服务端和客户端共用一套代码的方式称之为同构
    优点：解决了传统SPA项目首屏加载时间过长和不利于SEO的缺陷；
    缺点：SSR同样带来了服务器负担中，实施难度大等诸多问题；

    其他解决方案：
        如果对首屏加载时间和SEO没有极致的追求，我们可以选择更轻便的方案，如利用webpack和react-router分割代码，减少首屏加载时间；
        利用prerender进行预渲染，优化项目搜索引擎排名，不一定需要对整个项目采用同构的发给你是否i进行服务端渲染；

###46. React同构
    https://blog.csdn.net/MichelleZhai/article/details/118423494

###47. react-router history和hash的区别和比较
    hash（地址栏URL中的#）：
        原理：#后面的参数不作为请求路由，只是切换对应路由path对应的组件，每次hash变化时都会调用onhashchange事件；
        特点：hash虽然在URL中，但是不会被包括在HTTP，因为我们hash每次页面切换其实是切换#洁癖，后面的内容；
            而#后面的内容改变不会触发地址的改变，所以不存在向后台发送请求，对后端完全没有影响，因此改变hash不会导致重新加载页面；
        优点：可以随意刷新
    
    history（利用了浏览器的历史记录栈）：
        原理：利用HTML5 History Interface中新增的pushState()和replaceState方法；
        特点：在当前已有的back，forward，go的基础上，它们提供了对历史记录进行修改的功能，只是当它们执行修改时，
            虽然改变了当前的URL，但是浏览器不会立即向后段发送请求，htistory可以通过前进后退控制页面的跳转；
            刷新的是真实改变的url；
        缺点：不能刷新，需要后段进行配置，由于history模式是可以自由修改请求url，当刷新时如果对应地址进行匹配就会返回404，
            但是在hash模式下是可以刷的，前端路由修改的是#中的信息，请求地址是不会改变的；

###48. React中各种组件复用的优势和劣势
    mixin：变量作用来源不清，属性重名，minxins引入过多会导致顺序冲突；
    HOC和Render props：组件嵌套过多，不利于渲染调试，会劫持props，会有漏洞；
    hook：Hooks就是染你不必xieclass组件就可以使用state和其他React特性，也可以编写自己的hooks在不同的组件之间复用。
        代码量少，复用性高，易于拆分，也有一些闭包的坑；
###35. React的Fiber架构
    原有react页面渲染获取生命周期函数、对比VirtualDOM、最后更新DOM，全程都是同步操作，耗时过长，影响性能，所以引入fiber；
    Fiber分片，把耗时过长的任务分成很多小片，小片运行时间很短，每个小片执行之后都给其他任务一个执行的机会，这样唯一的线程就不会被独占，其他依然有运行的机会；
    Fiber架构主要引入了两个新的概念：
        一个是Time slicing时间分片，时间分片是利用了Fiber的可中断、可继续的功能，每个渲染周期内都会留一部分时间来响应用户的输入；
        二是Supsense，这两者用来应对cpu和网络问题，解决卡顿或者白屏问题；
###36. React性能优化
    Code splitting；
    shouldComponentUpdate避免重复渲染；
    异步按需加载，路由懒加载，路由监听器；
    组件尽可能进行拆分，解耦；
    列表类组件优化：
        比如：shouldComponentUpdate(nextProps, nextState)
        React.PureComponent
        Immutable
        React.memo
    bind函数优化：
    非可控组件和可控组件区别是否受state影响
    ReactDOMServer进行服务端渲染组件
###37. React新的生命周期，为什么getDerivedStatefromProps是静态的
    首先介绍一下React最新的生命周期执行过程：
        1. 挂载：
            constructor()
            static getDerivedStatefromProps(props, state)
            render()
            componentDidMount()
        2. 更新：
            static getDerivedStatefromProps(props, state)
            shouldComponentUpdate(nextProps, nextState, snapshot)
            render()
            componentDidUpdate()
        3. 卸载UnMounting阶段
            componentDidUnmount
###38. memoization
##顶层API - React
###39. 创建组件：
    可以使用React.Component或者React.PureComponent来定义React组件，或者使用React.memo将组件定义为可被包装的函数：
        React.Component：
            1. 组件的生命周期（挂载、更新、卸载）；
            2. 其他API（setState，forceUpdate）；
                用法：this.setState()，this.forceUpdate()
            3. class属性（defaultProps， displayName）:
                defaultProps：可以为 Class 组件添加默认 props，这一般用于 props 未赋值，但又不能为 null 的情况。
                displayName：字符串多用于调试消息
            4. 实例属性（props，state）；
        2. React.PureComponent
            PureComponent 与 Component 的区别在于 React.Component 并未实现 shouldComponentUpdate()，
            而 React.PureComponent 中以浅层对比 prop 和 state 的方式来实现了该函数。
            
            注意：
                PureComponent 中的 shouldComponentUpdate() 仅作对象的浅层比较。
                PureComponent 中的 shouldComponentUpdate() 将跳过所有子组件树的 prop 更新。因此，请确保所有子组件也都是“纯”的组件。
            
            使用场景：
                state中不存在复杂数据类型（object, array等）；
                且组件生命周期中可能出现无意义的重新渲染（更新前后props或者state与更新前相同）；
                
            补充：
                通俗解释：如果定义了 shouldComponentUpdate()，无论组件是否是 PureComponent，它都会执行shouldComponentUpdate结果来判断是否 update。
                    如果组件未实现 shouldComponentUpdate() ，则会判断该组件是否是 PureComponent，
                    如果是的话，会对新旧 props、state 进行 shallowEqual 比较，一旦新旧不一致，会触发 update。
                浅对比（shallowEqual）：通过遍历对象上的键执行相等性，并在任何键具有参数之间不严格相等的值时返回false。 当所有键的值严格相等时返回true。
        3. React.memo
            React.memo为高阶组件，作用与PureComponent类似，但是memo可以在函数组件中使用；
            
            如果你的组件在相同 props 的情况下渲染相同的结果，那么你可以通过将其包装在 React.memo 中调用，
            以此通过记忆组件渲染结果的方式来提高组件的性能表现。这意味着在这种情况下，React 将跳过渲染组件的操作并直接复用最近一次渲染的结果。
            
            React.memo 仅检查 props 变更。如果函数组件被 React.memo 包裹，且其实现中拥有 useState，useReducer 或 useContext 的 Hook，
            当 context 发生变化时，它仍会重新渲染。
            
            默认情况下其只会对复杂对象做浅层对比，如果你想要控制对比过程，那么请将自定义的比较函数通过第二个参数传入来实现
            
            参考：https://blog.csdn.net/weixin_42686892/article/details/112688981
            
            补充：父组件更新后，会重新渲染子组件，这个时候子组件接收到一个新的props，因此父组件更新后，会引起子组件更新；
###40. 创建React元素（简单了解）：
        在js中创建React元素可以使用 createElement 和 createFactory；
        但React建议使用JSX来编写UI组件，一般来说，如果你使用了 JSX，就不再需要调用这两个方法；
###41. 转换元素（简单了解）：
        1. cloneElement
        2. isValidElement
        3. React.children
###42. Fragments:
        React.Fragment 组件能够在不额外创建 DOM 元素的情况下，让 render() 方法中返回多个元素；
        也可以使用其简写语法<></>。
###43. Refs:
        React.createRef：创建一个能够通过 ref 属性附加到 React 元素的 ref。
        React.forwartRef：
            会创建一个React组件，这个组件能够将其接受的 ref 属性转发到其组件树下的另一个组件中。
            这种技术并不常见，但在以下两种场景中特别有用（详见Refs转发）：
               1. 转发 refs 到 DOM 组件
               2. 在高阶组件中转发 refs
###44. Suspense：
        React.lazy：
            React.lazy() 允许你定义一个动态加载的组件。这有助于缩减 bundle 的体积，并延迟加载在初次渲染时未用到的组件。
        React.Suspense
            React.Suspense 可以指定加载指示器（loading indicator），以防其组件树中的某些子组件尚未具备渲染条件。
            目前，懒加载组件是 <React.Suspense> 支持的唯一用例：
###45. React Hooks（见React Hooks）

##顶层API - ReactDOM：
###46. ReactDOM方法
    react-dom 的 package 提供了可在应用顶层使用的 DOM 方法：
    1. render()
        用法：ReactDOM.hydrate(element, container[, callback])
        作用：用于将模版转换成HTML语言,渲染DOM,并插入指定的DOM节点中；
    2. hydrate()
        用法：ReactDOM.hydrate(element, container[, callback])
        作用：与 render() 相同，但它用于在 ReactDOMServer 渲染的容器中对 HTML 的内容进行 hydrate 操作。
            React 会尝试在已有标记上绑定事件监听器。
    3. unmountComponentAtNode()
        用法：ReactDOM.unmountComponentAtNode(container)；
        作用：从 DOM 中卸载组件，会将其事件处理器（event handlers）和 state 一并清除。
            如果指定容器上没有对应已挂载的组件，这个函数什么也不会做。如果组件被移除将会返回 true，如果没有组件可被移除将会返回 false。
    4. findDOMNode()
        findDOMNode 是一个访问底层 DOM 节点的应急方案（escape hatch）。
        在大多数情况下，不推荐使用该方法，因为它会破坏组件的抽象结构。严格模式下该方法已弃用。
    5. createPortal()
        用法：ReactDOM.createPortal(child, container)；
        作用：创建 portal。Portal 将提供一种将子节点渲染到 DOM 节点中的方式，该节点存在于 DOM 组件的层次结构之外。
## 顶层API - ReactDOMServer
###47. ReactDOMServer
    ReactDOMServer 对象允许你将组件渲染成静态标记。通常，它被使用在 Node 服务端上：    
    
    下述方法可以被使用在服务端和浏览器环境：
        renderToString()
        renderToStaticMarkup()
        
    下述附加方法依赖一个只能在服务端使用的 package（stream）。它们在浏览器中不起作用：
        renderToNodeStream()
        renderToStaticNodeStream()
###48. 代码分割（路由懒加载）
    对你的应用进行代码分割能够帮助你“懒加载”当前用户所需要的内容，能够显著地提高你的应用性能。
    尽管并没有减少应用整体的代码体积，但你可以避免加载用户永远不需要的代码，并在初始加载的时候减少所需加载的代码量。
    参考 https://blog.csdn.net/weixin_45679977/article/details/107785105
        https://webpack.docschina.org/guides/lazy-loading/#root
###49. Context
    作用：Context 提供了一个无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。
    目的是为了共享那些对于一个组件树而言是“全局”的数据，例如当前认证的用户、主题或首选语言;
    
    API：
        React.createContext:
            用法：const MyContext = React.createContext(defaultValue)
            作用：创建一个 Context 对象。当 React 渲染一个订阅了这个 Context 对象的组件，
                这个组件会从组件树中离自身最近的那个匹配的 Provider 中读取到当前的 context 值。
                只有当组件所处的树中没有匹配到 Provider 时，其 defaultValue 参数才会生效。
                此默认值有助于在不使用 Provider 包装组件的情况下对组件进行测试。
                注意：将 undefined 传递给 Provider 的 value 时，消费组件的 defaultValue 不会生效。
        Context.Provider:
            用法：<MyContext.Provider value={value}> ... </MyContext>    
            作用：每一个Context对象都会返回一个Provider React组件，它允许消费组件订阅Context的变化；
            注意：通过新旧值检测来确定变化，使用了与 Object.is 相同的算法。
        Class.contextType:
            用法：MyClass.contextType = MyContext;
            作用：挂载在 class 上的 contextType 属性会被重赋值为一个由 React.createContext() 创建的 Context 对象。
                此属性能让你使用 this.context 来消费最近 Context 上的那个值。你可以在任何生命周期中访问到它，包括 render 函数中。    
        Context.Consumer：
            用法：<MyContext.Consumer> {value => ...} </MyContext.Consumer>
                这种方法需要一个函数作为子元素（function as a child）。这个函数接收当前的 context 值，并返回一个 React 节点。
                传递给函数的 value 值等价于组件树上方离这个 context 最近的 Provider 提供的 value 值。
                如果没有对应的 Provider，value 参数等同于传递给 createContext() 的 defaultValue。
        Context.displayName:
            用法：MyContext.displayName = 'MyDisplayName';
            作用：context 对象接受一个名为 displayName 的 property，类型为字符串。
                React DevTools 使用该字符串来确定 context 要显示的内容。
    补充：如果只是想避免层层传递一些属性，可以采用组件组合的方式代替context；
        而如果子组件需要在渲染前和父组件进行一些交流，你可以进一步使用 render props。
###50. Refs转发
    作用：Ref 转发允许某些组件接收 ref，并将其向下传递（换句话说，“转发”它）给子组件。
    目的：上层组件可以获取底层DOM的ref，并通过调用ref方法来直接操作底层DOM；
    
    使用方式：
        1. 在父组件中通过React.createRef()创建一个ref并将其作为props传递给子组件；
        2. 使用React.forwardRef(callback)包裹子组件；
        3. callback中传入props和ref，返回子组件；
        4. 可将ref绑定至子组件的DOM节点中，此后便可以在父组件中通过ref.current操作底层DOM元素；
###51. 高阶组件（HOC）
    概念：高阶组件（HOC）是 React 中用于复用组件逻辑的一种高级技巧。
        HOC 自身不是 React API 的一部分，它是一种基于 React 的组合特性而形成的设计模式。
        简而言之，高阶组件是一种参数为组件、返回值为新组件的函数； 
        
    高阶组件是什么？
        高阶组件是重用组件逻辑的高级方法，是一种源于 React 的组件模式。 
        HOC 是自定义组件，在它之内包含另一个组件。它们可以接受子组件提供的任何动态，
        但不会修改或复制其输入组件中的任何行为。你可以认为 HOC 是“纯（Pure）”组件。    
    
    高阶组件可以做什么？
        代码重用，逻辑和引导抽象
        渲染劫持
        状态抽象和控制
        props控制
    
    注意：
        不要在 render 方法中使用 HOC；
        务必复制静态方法；
        Refs 不会被传递；
###52. Render Props
     Render Props是指一种在 React 组件之间使用一个值为函数的 prop，从而实现共享代码的简单技术；
     使用 Render Props 来解决横切关注点（Cross-Cutting Concerns）
     使用 Props 而非 render
     
     注意：将 Render Props 与 React.PureComponent 一起使用时要小心；
        如果你在 render 方法里创建函数，那么使用 render prop 会抵消使用 React.PureComponent 带来的优势。
        因为浅比较 props 的时候总会得到 false，并且在这种情况下每一个 render 对于 render prop 将会生成一个新的值。
###53. 受控组件和非受控组件
    1. 受控组件没有维持自己的状态，非受控组件保持自己的状态；
    2. 受控组件数据由父组件控制，非受控组件数据由DOM控制；
    3. 受控组件通过props获取当前值，非受控组件通过ref获取值；

#React hooks
###54. React加入Hooks的意义是什么，为什么要加入这一特性？
    加入Hooks是为了解决一些类组件中出现的问题：
        1. 组件之间的逻辑状态难以复用；
        2. 大型复杂的组件难以拆分；
        3. Class语法的使用不友好（this指针问题）；
    有了Hooks之后，可以不必写class组件，就能使用到类组件的特性；
    同时也可以编写分自己的hooks，在不同的组件之间复用；
    
###55. Hooks优点和缺点：
    优点：
        1. 没有破坏性改动：完全可选，无需重写任何代码便可以在一些代码中尝试hooks，100%向后兼容；
        2. 更容易复用代码：通过自定义hooks来复用逻辑代码，可以解决类组件逻辑难以复用的问题；
        3. 函数式编程风格：函数式组件，状态保存在运行环境，每个功能都保存在函数中，整体风格更加清爽、优雅；
        4. 代码量少，复用性高，可读性强；
        5. 更加容器拆分； 
    缺点：
        1. 状态不同步（闭包带来的坑）：函数的运行是独立的，每个函数都有一份独立的闭包作用域，当我们处理复杂逻辑时，经常会遇到"引用不是最新的"的问题；
###56. 为什么不能在循环、条件或者嵌套函数中调用hooks
    不要在循环，条件或嵌套函数中调用Hook，必须始终在React函数的顶层使用Hook。
    这是因为React需要利用调用顺序来正确更新相应的状态，以及调用相应的钩子函数。
    一旦在循环或条件分支语句中调用Hook，就容易导致调用顺序的不一致性，从而产生难以预料到的后果。
    
    hooks在初始化时候是以链表形式存储的，后续更新都是按照这个链表顺序执行的
###57. 如何解决hooks闭包的问题；
    问题：每次 render 都有一份新的状态，数据卡在闭包里，捕获了每次 render 后的 state，也就导致了输出原来的 state；
    解决：可以通过 useRef 来保存 state。前文讲过 ref 在组件中只存在一份，无论何时使用它的引用都不会产生变化，因此可以来解决闭包引发的问题。
###58. 常用的hooks有哪些
    
###59. useEffect为什么有时候会出现无限重复请求的问题；
    可能1：在Effect中做数据请求时未设置依赖参数，同时在Effect更新了状态；
    可能2：所设置的effect总是在改变；
    
    解决：使用useCallback()或者useMemo()包裹useEffect；
###60. React Hook Api 原理
###61. useEffect如何模拟生命周期
    1. componentDidMount：第二个参数传入空数组；
    2. componentDidMount 和 componentDidUpdate: 不传入第二个参数；
    3. componentWillUnmount: useEffect函数体中返回一个函数；
    
###62. Hooks模拟的生命周期函数和真实的生命周期函数有什么区别
    1. 模拟的componentWillUnmount和真实的componentWillUnmount有本质区别：模拟的清理函数在每次调用useEffect前都会执行；并不是组件卸载时候才执行；
    2. useEffect在副作用结束之后，会延迟一段时间执行，并非同步执行，和compontDidMount有本质区别。遇到dom操作，最好使用useLayoutEffect。
###63. Hooks相比HOC和render props有什么优点
    HOC和render props都是一种开发模式，将复用逻辑提升到父组件，容易嵌套过多，过度包装；
    hooks是react的api模式，将复用逻辑提取到顶层，而不是强行提升到父组件，这样就可以避免HOCheRender Props中出现的嵌套地狱；
###64. 函数式组件和类组件的区别
    对于类组件来说：
        首先state是不可变的，setState后生成一个全新的引用；
        但是类组件每次都会通过this.state来读取状态，所以每次代码执行都会拿到最新的state；
    对于函数式组件来说：
        useState产生的数据也是不可变的，通过数组的第二个参数set一个新的值之后，原来的值在下次渲染时会形成一个新的引用；
        但它的state没有通过this的方式获取，每次执行都会读取当时渲染闭包环境的数据，虽然最新的值跟着最新的渲染变了，但是在旧的渲染里，状态依旧是旧值；
    
    1. 原理：function组件能够捕获渲染的值，读取渲染闭包内的数据，
        而class组件在react通过this的方式读取，this是可变的，所以总能获取到最新的props；
    2. 保存状态：class把state属性挂载的对象保存到memoizedState属性中，
        而Function组件是用链表来保存状态的，memoizedState属性保存的事链表的头指针；

###65. useEffect 和 useLayoutEffect的区别
    1. useEffect是render结束后，callback函数执行，但是不会阻塞浏览器的渲染；
        但是classcomponentDidMount 和 componentDidUpdate 是同步的，在render结束后就运行；
        useEffect在大部分情况下都会比class的方式性能更好；
    2. useLayoutEffect使用在处理DOM的时候，当你的useEffect里面的操作需要处理DOM，
        并且会改变页面的样式，就需要使用这个，否则可能会出现闪屏现象，
        useLayoutEffect里面的callback函数会在DOM更新完成后立即执行，但是会在浏览器进行渲染前运行完成，阻塞了浏览器的渲染；

###66. useState 和 setState 的区别
    1. setState可以在第二个参数中传入回调，useState里面的setState则没有第二个参数；
    2. useState通过数组第二个参数set一个新值后，新值会形成一个新的引用，捕获当前渲染闭包里的数据state；
        setState是通过this.state读取state，每次代码执行都会拿到最新的state引用；

###67. useReducer 和 redux 的区别
    1. useReducer()提供了状态管理，其基本原理是通过用户在页面中发起action, 从而通过 reducer方法来改变state, 
        从而实现页面和状态的通信,使用很像redux
    2. useReducer是useState的代替方案，用于state复杂变化
    3. useReducer是单个组件状态管理，组件之间通信还需要通过props；
    4. redux是全局的状态管理，多组件共享数据；
###68. 如何自定义hook
###69. Hooks性能优化
    useMemo缓存数据；
    useCallback缓存函数；
###70. 如何在高阶组件中访问组件实例
    1、属性代理。高阶组件通过包裹的React组件来操作props，更改 props，
    可以对传递的包裹组件的WrappedComponent的props进行控制

    2、通过 refs 获取组件实例

#2.Redux相关




#3.React Router相关





