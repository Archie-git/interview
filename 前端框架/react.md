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
###7. 
