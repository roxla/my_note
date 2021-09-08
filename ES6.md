##### ES6模块化规范中定义：

> -     每个js文件都是一个独立的模块
> -     导入其他模块成员使用<span style="color: red;">import</span>关键字
> -     向外共享模块成员使用<span style="color: red;">export</span>关键字
>

##### 在node.js中体验ES6模块化

> node.js中默认仅支持CommonJS模块化规范，若想基于node.js体验ES6的模块化语法，可以按照如下两个步骤进行配置
>
> 1. 确保安装了v14.15.1或更高版本的node.js
> 2. 在package.json的根节点中添加 "type":"module"节点

##### ES6模块化的默认导出和导入

> **默认导出**：
>
> 默认导出的语法：<span style="color: red;">export default</span> <span style="color: #329BDC;">默认导出成员</span>
>
> ```javascript
> len n2 = 10 // 定义模块私有成员 n1
> len n2 = 20 // 定义模块私有成员 n2（外界访问不到 n2，因为它没有被共享出去）
> funciton show(){} // 定义模块私有方法 show
> 
> export default { // 使用 export default 默认导出语法，向外共享 n1 和 show 两个成员
>  n1,
>  show
> }
> ```
>
> <span style='color: red;'>默认导出的注意事项：</span>每个模块中，<span style='color: #329BDC; text-decoration:underline;'>只允许使用唯一的一次</span> export default，否则会报错！
>
> 
>
> 默认导入：
>
> 默认导入的语法：<span style="color: red;">import</span> <span style="color: #329BDC;">接受名称</span> <span style="color: red;">from</span> '<span style="color: #329BDC;">模块化标识符</span>'
>
> ```javascript
> // 从 01_m1.js 模块中导入 export default 向外共享的成员
> import m1 from './01_m1.js'
> 
> // 打印输出的结果为：
> //{ n1: 10, show: [Function: show] }
> console.log(m1)
> ```
>
> <span style='color: red;'>默认导入的注意事项：</span>默认导入时的接收名称可以任意名称，<span style="color: #329BDC;">只要是合法的成员名称即可</span>

