# Vue.js 框架最为核心的 Virtual DOM 是如何实现的？> 【作业】测一测 + 练一练

### 下面关于虚拟 DOM 的说法正确的是：D
### 下面关于 Snabbdom 库的描述错误的是：D

## 简答题
### 请简述 patchVnode 函数的执行过程。
1. 执行用户设置的prepatch钩子函数
2. 判断新老节点是否相同，相同则直接返还，不相同则继续执行
3. vnode如果定义了data, 执行模块和用户设置的钩子函数
4. 对比新旧节点
   + 如果vnode.text未定义
        - 如果新老子节点都有定义，对比新老子节点，不相同则更新子节点
        - 如果新子节点有定义而老子节点未定义
            + 老节点有text，清空dom内容
            + 批量添加子节点
        - 如果老子节点有定义，而新子节点未定义，批量移除子节点
        - 如果老节点有text属性，清空dom内容
   + 如果定义了vnode.text且oldVnode.text不等于它
        - 如果老节点有children，移除children，
        - 设置textCOntent为vnode.text

5. 执行用户设置的postpatch钩子函数