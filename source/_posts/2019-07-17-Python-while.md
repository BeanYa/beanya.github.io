---
title: Python--while的循环控制
date: 2019-07-17 17:50:10
categories:
- Python
tags:
- Python
- Note
---
## 什么是循环

举个栗子，你现在很闲，就想写一个python程序，看着他一直打印`Hello World`然后发呆。

怎么办呢？

总不能你要看一百万行的`Hello World`就复制粘贴打一百万行的`print('Hello World')`吧？

所以就需要`while`和`for`循环来控制，循环重复的执行一段代码。

本文先只讲解`while`，`for`其实也是等效的。

## 补充知识

`if`语句叫做条件控制语句

`while`、`for`叫做循环控制语句

两个都是`流程控制`的部分，代码是从头到尾顺序执行的，有一定的流程，而流程的控制就交给了`if`、`while`和`for`三种语句。

### while的流程图

![](https://www.runoob.com/wp-content/uploads/2014/05/while_loop_1.png)

流程图可以解析成对应的`while`语句：

``` python
while condition:
    statement
    statement
    ...
    statement
further statement
```

上面的further stateme和script都是一样的，表示接下来的代码。

## while的例子

runoob(菜鸟教程)上关于循环的例子还是比较生动的

![](https://www.runoob.com/wp-content/uploads/2014/05/006faQNTgw1f5wnm06h3ug30ci08cake.gif)

## 约定

成立的意思就是：布尔值为真（True）

不成立的意思就是：布尔值为假（False）

文章中可能时而会说成立，时而说真/假，意思是一样的，请自行代换。

## while

`while`的形式：

* 
    ``` python
    while 判断条件:
        要循环的代码块
    ```

* 
    ``` python
    while 判断条件:
        要循环的语句A
        要循环的语句B
        ...
    ```

之前讲的代码块里，其实若干条相同缩进量的代码就是一个代码块。

也就是说这两种`while`是一样的，仅仅列出来提及一下代码块的知识。

>注意：语句A和语句B的缩进要相同，这样程序才会认为他们都是同级并且都是属于while的代码块的。

上面两个例子中，不论是第一种的代码块还是第二种的n个语句，正确缩进的情况下，他们都是属于`while`语句的，把这个代码块（n个语句）称之为`while`语句的`循环体`

判断条件是一个布尔表达式，也可以直接是一个布尔值。

例如：

``` python
print('Go')
while 1<2:
    print('Hello World')
    print('Done')
print('exit this program')
```

判断的条件就是`1<2`这个布尔表达式，程序是这样执行的:

1. 先执行`print('Go')`，我用来表示程序要开始执行了。
2. 碰到`while`语句了，会先计算`while`语句的条件（表达式）的布尔值是真（True）还是假（False）
3. 计算`1<2`的值，发现它是`True`，也就是说`while`语句的条件是成立的
4. 去执行`while`语句里的循环体，也就是两行`print`
5. 执行完毕后，回到`步骤(3)`，检查`while`的条件是不是成立的，发现它还是`True`,回到`步骤(4)`

> 步骤(1)是用来表示程序要开始执行了，与`while`无关

因为`1<2`是永远成立（布尔值为True）的，也就是`while`的条件是一直为`True`的，这个循环会一直执行，循环体外的`print('exit this program')`，被忽略了，直到程序被关闭，这种情况也称之为`死循环`。

但是大多数都不会去写一个死循环的`while`，因为后面的代码都废掉了，程序会一直在`while`里转圈圈，出不来。

另一个例子：

``` python
print('Go')
a = 0
while a<1000:
    print('Hello World')
    print('Done')
    a = a + 1
print('exit this program')
```

可以看到，在`while`的循环体里执行修改条件里用到的变量是很常见的，循环体执行完之后都会去重新判断条件是否成立，不成立就跳出这个`while`循环，成立就重新执行循环体。

上面的这个例子里，a一开始是0，循环体的最后一个语句：将`a`的值加1，并将新的值赋回给`a`，那么在循环1000次之后，`a`的值变成了1000,而`1000<1000`是不成立的，也就是说`while`语句的条件不成立了，那么退出`while`语句，去执行`print('exit this program')`

所以，当python顺序执行下来，碰到了`while`循环的执行顺序如下：

1. 判断`while`的条件是否成立
   >布尔表达式的值是否为真，也就是True）
2. 如果条件成立，执行`步骤(3)`和`步骤(4)`，否则执行`步骤(5)`
3. 执行`while`里面的循环体
   >上面例子中的`print('Hello World')`和`print('Done')`组成了`while`的循环体
4. 执行完循环体之后，计算执行完语句后`while`的条件是否还成立，如果成立，回到`步骤(3)`，否则执行`步骤(5)`
5. 执行`while`外面的代码块
   >上面例子中的`print('exit this program')`