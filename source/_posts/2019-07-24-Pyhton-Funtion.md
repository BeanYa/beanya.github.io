---
title: Pyhton-Funtion
date: 2019-07-18 16:40:32
categories:
tags:
---
## 为什么讲函数

函数其实想放到后面讲的，但是因为`for`循环会讲到`range()`这个函数，所以先基础的讲一下函数是什么。

## 什么是函数？

函数的严格定义是：将给定的输入，按照一定的映射关系，映射到一定的输入。

通俗来讲，其实就像流水线，你给我一些原料，我按照规定好的流程，制作出一些产品，这些产品都是一样的。

如果第一批产品和第二批产品产生了不同，那么应该都是来自于原料的不同。

也可以这样认为，函数其实就是一大段重复的代码块。

例如，在一个软件里面，我需要打印5行不同的信息：

``` python
Hello
What
I dont 
know
really?
```

python实现：


``` python
print('Hello')
print('What')
print('I dont')
print('know')
print('really?')
```

如果要重复打印这五行字，那么由之前的循环可以知道，当然是为这五行打印加上循环。

``` python
a = 0
while a<10:
    print('Hello')
    print('What')
    print('I dont')
    print('know')
    print('really?')
    a = a + 1
```

那么，如果我想打印n次这5行字后，打印其他的若干行，再回来打印这五行字，可能会变成这样：

``` python 
a = 0
while a<10:
    print('Hello')
    print('What')
    print('I dont')
    print('know')
    print('really?')
    a = a + 1

b = 0
while b<10:
    print('something else')
    print('yep')

c = 0
while c<10:
    print('Hello')
    print('What')
    print('I dont')
    print('know')
    print('really?')
    c = c + 1
```

有没有发现，其实三个循环的第一和第三个循环除了用于判断的变量名字不一样之外，是不是完全一样呢？

那么可以把这两个完全一样，或者称之为重复的代码片段，提取出来，提取出来后就被称之为函数了。

用函数的思路把上面的例子改进一下，会变成：

``` python
def print_my_words():
    a = 0
    while a<10:
        print('Hello')
        print('What')
        print('I dont')
        print('know')
        print('really?')
        a = a + 1

print_my_words()

b = 0
while b<10:
    print('something else')
    print('yep')

print_my_words()
```

会发现变得简洁了很多。

>其实`print`就是一个函数，在前面`print('hello world')`的时候，就已经接触到什么是函数了。
>
>对于这个函数来说，`print`是他的函数名，小括号里的`'hello world'`是他的函数参数，至于什么是参数，下面讲解

在python里，函数的使用方法是：`函数名(参数)`，和变量名的区别就是有无小括号和括号里的参数。

例如，`a()`是调用函数`a`

而，`a`是声明一个变量`a`

## 编写函数的思路

编写函数最简单的思路就是，提取重复。

或者就像数学里头称的函数一样的思路，给定变量，返回结果。

小学都学过加法：`1+1=2`，而其实在数学里，这个算式可以被抽象为`f(1,1)=2`。

`f(1,1)`其实与python里的函数没有本质的区别。

可以看做是函数名为`f`的函数，他的`参数列表`有两个`参数`，分别是`1`和`1`。

而函数的内容，也就是函数体，就是在做两个参数相加的过程，也就可以得到一个相加函数：

``` python
def add(x,y):
    return x + y
```

## 函数形式和关键词的作用