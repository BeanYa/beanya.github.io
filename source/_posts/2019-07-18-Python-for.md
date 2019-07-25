---
title: Python-for循环
date: 2019-07-18 17:40:32
categories:
- Python
tags:
- Python
- Note
---
## 什么是 for ？

`for`和`while`一样，都是流程控制中控制循环的语句。

## 为什么有了 while 还要 for ？

现在有一个`while`循环，他的目的是执行一百次的`print('Rush B!')`

``` python
a = 1
while a <= 100:
    print('Rush B!')
    a = a + 1
```

但是有没有觉得，每次都要先声明一个变量`a`，还要在循环体里让他加`1`，是不是有些繁琐呢？

`for`循环就可以省略这样的步骤

同样的功能，用`for`的实现是这样的：

``` python
for a in range(100):
    print('Rush B!')
```

省去了变量`a`的提前声明，但是`a`在循环体里仍然是可以被访问的：

``` python
for a in range(100):
    print('Rush B!')
    print('%s times!' % a)
```

其中`range(100)`是一个函数，可以生成从`0 - 99`的数字序列，也就是100个数。

为什么是用`range(100)`来生成序列，下面讲解。

## for 是怎么工作的？


