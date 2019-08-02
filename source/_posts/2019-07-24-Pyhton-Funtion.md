---
title: Pyhton-Funtion
date: 2019-07-18 16:40:32
categories:
tags:
---
## 为什么讲函数

函数其实想放到后面讲的，但是因为`for`循环会讲到`range()`这个函数，所以先基础的讲一下函数是什么。

## 什么是函数？

函数其实就是一段可以被重复使用的代码，用参数来代替其中的可变部分。

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

python中一个函数的形式如下：

``` python
def functionname( parameters ):
    "function_docstring"
    function_body
    return [expression]
```


`def`关键字是define的缩写，即 “定义”。

`functionname`就是函数的名字，一般是要求符合命名规则，命名规则在变量和数据类型有提及，刚入门不要求记忆，随便命名既可，但要`具意命名`，例如打印函数就叫`print`

> 具意命名就是名字和具体代表的东西要一致，用来表示名字的变量就叫`name`，用做加法的函数就叫`add()`

其中`"function_docstring"`是对函数的说明，运行的时候会跳过。

`function_body`就是函数体，也是一块可以被重复使用的代码块。

`return` 表示将某个值返回的意思，例如写一个加法函数，要把最后结果保存下来，就会把结果值返回。

下面是一个加法函数的例子：

``` python
def add_two_number(first, second):
    result = first + second
    return result
```


上面例子里，有两个参数，`first`和`second`，参数其实就是外来的变量，也是在函数中可变的部分。

这个函数的目的是做加法，加法的结果由两个数影响，这两个数是可变的，但是加法的过程是确定的。

所以，这两个数就是函数的参数了。

`return result`这一句的意思是把`result`变量返回，函数体运行结束后，需要把结果返回给调用者，也就是`return`的作用。

函数被定义，就是需要被使用的，使用的过程被叫做`函数的调用`

那么，怎么调用一个函数呢？

在“Hello World”的例子里：

``` python
print('Hello World')
```

其实就是调用了一个函数`print`，`'Hello World'`是他的参数。

上面例子里的加法函数的调用例子如下：

``` python
def add_two_number(first, second):
    result = first + second
    return result

a_number = add_two_number(1,2)

print(a_number)
```

`add_two_number(1,2)`就是调用了这个函数，参数分别是`1`和`2`，按顺序对应。

可以分解的看成，`a_number = add_two_number(1,2)`这个语句的执行步骤被分成了四部分：

1. a_number = add_two_number(1,2)
2. 执行跳到add_two_number的代码块来，执行对参数的赋值，也就是`first = 1`和`second = 2`
3. 执行函数体
4. 返回结果

函数的`返回值`，可以看做执行后，把赋值语句替换掉，也就是`a_number = add_two_number(1,1)`替换成`a_number = 3`

然后`print(a_number)`的结果就是打印了`3`