# web-interview
前端面试题总结

# HTML中行内元素已块级元素的区别
1、行内元素与块级元素可以相互转换，通过修改display属性值来切换元素和行内元素，行内元素display:inline，块级元素display:block;
2、行内元素和其他行内元素都会在一条水平线上排列，都是在同一行的；块级元素却总是会在新的一行开始排列，各个块级元素独占一行，垂直向下排列，若想使其水平方向排列，可使用左右浮动，让其水平方向排列。
3、行内元素不可以设置宽度，宽度高度随文本内容的变化而变化，但是可以设置行高，同时在设置外边距margin上下无效，左右有效，内填充padding上下无效，左右有效，块级元素可以设置宽度，并且宽度高度以及外边距，内填充都可随意控制。
4、块级元素可以包含行内元素和块级元素，还可以容纳内联元素和其他元素，行内元素不能包含块级元素，只能容纳文本或者其他行内元素。

# 什么是闭包
简单来说，闭包是指可以访问另一个函数作用域变量的函数，一般是定义在外层函数中的内层函数。
函数作用域
内存回收机制
作用域继承

#  为什么需要闭包呢
局部变量无法共享和长久的保存，而全局变量可能造成变量污染，所以我们希望有一种机制既可以长久的保存变量又不会造成全局污染。


# 闭包的作用是什么？
保护
保存

# 闭包的运用场景
设计私有的方法和变量

# 特点
即想反复使用，又想避免全局污染

# 闭包的注意事项
通常，函数的作用域及其所有变量都会在函数执行结束后被销毁，但是，在创建了一个闭包以后，这个函数的作用域就会一直保存到闭包不存在为止。

# 闭包的缺陷
闭包的缺点就是常驻内存会增大内存使用量，并且使用不当很容易造成内存泄露
如果不是因为某些特殊任务而需要闭包，在没有必要的情况下，在其他函数中创建函数是不明智的，因为闭包对脚本性能具有负面影响，包含处理速度和内存消耗。



