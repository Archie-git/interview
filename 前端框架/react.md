### https://blog.csdn.net/eyeofangel/article/details/88797314
### https://blog.csdn.net/MichelleZhai/article/details/118423494
### hooks：https://blog.csdn.net/MichelleZhai/article/details/118392437

###1. 区分RealDOM和VirtualDOM
    1. RealDOM更新缓慢、VirtualDOM更新迅速；
    2. RealDOM可以直接更新HTML，Virtual无法直接更新HTML；
    3. RealDOm中如果元素更新，则会创建新的DOM，VirtualDOM中如果元素更新，则会更新JSX；
    4. RealDOM的DOM操作代价很高，VirtualDOM的DOM操作非常简单；
    5. RealDOM消耗内存多，VirtualDOM消耗内存少；
###2. 什么是React
    React是Facebook在2011年开发的前端Javascript库；
    它遵循于组件的方法，有助于构建可重用的UI组件；
    它用于开发复杂和交互式的Web和移动UI；
    React拥有一个很大的支持社区；
###3. React有什么特点
    它使用虚拟DOM，而不是真正的DOM；
    它可以用服务端渲染；
    它遵循单项数据流和数据绑定；
###4. React的主要优点
    高性能
    组件化
###5. 说一下Virtual DOM的工作原理
    VirtualDOM是一个轻量级的Javascript对象，它最初只是real DOM的副本，
    它是一个节点树，它将元素、它们的属性和内容作为对象及其属性。
    React的渲染函数从React组件中创建一个节点树，然后他响应数据模型中的变化来更新该树，该变化是由用户或者系统完成的各种动作引起的。

    VirtualDOM工作过程有三个简单的步骤：
    1. 每当底层数据发生改变时，整个UI都将在VirtualDOM描述中重新渲染；
    2. 然后计算之前DOM表示与新表示之间的差异；
    3. 计算完成之后，将只用实际更改的内容更新real DOM
###6. 为什么浏览器无法读取JSX
    浏览器只能处理Javascript对象，而不能读取常规Javascript对象中的JSX，所以，为了使浏览器能够
    读取JSX，首先，需要用像Babel这样的JSX转换器将JSX文件转换成Javascript对象，然后再将其传给浏览器；
###7. 如何理解，在React中，一切都是组件这句话
    组件是React应用UI的构建块，这些组件将整个UI分成小的独立并可重用的部分，每个组件彼此独立，二不会影响UI的其余部分；
###8. 解释React中render()的目的；
    每个React组件强制要求必须有一个render，它返回一个React元素，是原声DOM组件的表示；
###9. 什么是props
    Porps是React中属性的简写，它们是只读属性，必须保持不可变，
    它们在整个应用当中总是从父组件传递到子组件，子组件永远不能将props送回父组件，
    这有助于维护单项数据流，通常用于呈现动态生成的数据；
###10. React中的状态是什么，它是如何使用的
    状态是React组件的核心，是数据的来源，必须尽可能简单；
    基本上状态是确定组件呈现和行为的对象，与props不同，它们是可变的，以便与创建动态和交互式组件；
###11. React组件的生命周阶段是什么
    1. 初始化渲染阶段：这个是组件从创建到挂在到DOM上的阶段
    2. 更新阶段：组件被挂载到DOM之后，当prop或者状态发生改变时，才会引起更新和重新渲染；
    3. 卸载阶段：这是组件声明周期的最后阶段，组件被销毁并从DOM中删除；
###12. React组件生命周期方法
###13. React refs
###14. React refs使用场景
    需要管理焦点、选择文本或者媒体播放时
    触发式动画
    与第三方DOM库集成
###15. 受控组件和非受控组件
###30 什么是高阶组件
###31 高阶组件可以做什么
###32 React中Key的重要性
    key用于识别唯一的VirtualDOM元素以及驱动UI的相应数据，它们通过回收DOM中当前所有的元素来帮助React优化渲染。
    这些key必须是唯一的数字或者字符串，React只是重新排序元素而不是重新渲染它们，这样可以提高应用程序的性能；
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



















