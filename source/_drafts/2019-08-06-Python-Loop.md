---
title: Python-循环和if更进一步
categories:
  - Python
tags:
  - Python
  - Note
date: 2019-08-06 01:47:52
---
## 讲的What？

本章主题是，`while`和`for`循环，还有`if`的嵌套。

## 为什么讲嵌套？

先从`if`的嵌套开始。

前面学过了，`if`的形式就是那几种，最简单的就是：

``` python
if bool_expression:
    statements()
```

那么，举个例子！

让我们把例子的复杂度稍稍提高一下，并且贴近一下生活。

现在，你要去美团买演唱会的票，但是你们是四人行，四个好兄弟，只能一起行动，缺谁都8行。

并且，打印你的买票心理活动。

那么，能够买到票的前提是：

1. 起码有4张票可以买
2. 口袋里的钱够用

思考一下，是你的话需要怎么编写这个程序？

如果没想好第一步，那么就从变量声明开始吧！

如果还是不知道怎么开始。

那么下面给你开始的代码：

``` python
available_ticket = 3
ticket_price = 100
pocket_money = 500
...你的if语句...
...若干个print()...
```

可以自己思考一下，写得出来可以发出来瞧瞧。

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

当然，以下是参考答案。

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### 参考答案

``` python
available_ticket = 3    #可用的票数
ticket_price = 100      #票价
pocket_money = 500      #口袋里的小钱钱
if available_ticket >= 4:
    print('票够')
    if ticket_price * 4 <= pocket_money:
        print('可以了，冲锋！')
    else:
        print('啊哦，钱不够了')
else:
    print('没票了')
```

你可以修改上面的三个变量来打印不同的结果。

### if的嵌套

上面的参考答案里头，你可以看到，第一个`if`，也就是判断票是否够的那一片代码块里，又嵌套了另一个`if`，用于判断口袋里的钱是否够买4张票。

为什么要`嵌套`呢？

因为按照正常思路，如果票不够，那我也就不用考虑口袋里的钱是否够用的问题。

所以整个的思路是这样的：

1. 票够不够？
2. 票够，那口袋里的钱够不够呢？
   1. 如果够，就打印`可以了，冲锋！`
   2. 如果不够，就打印`啊哦，钱不够了`
3. 不够就打印`没票了`，并且结束程序.

这是一个渐进式的思路，在第一个判断成立的条件下，再进行判断第二个条件是否成立，因为第二个条件跟第一个条件不成立时无关（不考虑）。

这就是`嵌套`。

可以把例子里的：

``` python
    print('票够')
    if ticket_price * 4 <= pocket_money:
        print('可以了，冲锋！')
    else:
        print('啊哦，钱不够了')
```

看做是一个独立的`代码块`，他们拥有相同的`缩进量`。

> 上面的两个可能因为渲染问题，显示出来是顶格的，我想展示出的是带有一个tab缩进的代码块。就像下面的例子里去掉第一行。

下面的：

``` python
    print('没票了')
```

也是一样的道理。

其实，可以看做是在另一个代码块里再写一个普通的`if`。

然后，从上面的一个`if`来说，就是一个嵌套的`if`：

``` python
if available_ticket >= 4:
    print('票够')
    if ticket_price * 4 <= pocket_money:
        print('可以了，冲锋！')
    else:
        print('啊哦，钱不够了')
```

当然，不是只能在`if`里写嵌套，`else`也可以。

对参考答案进行等效的转换：

``` python
if available_ticket < 4:
    print('没票了')
else:
    print('票够')
    if ticket_price * 4 <= pocket_money:
        print('可以了，冲锋！')
    else:
        print('啊哦，钱不够了')
```

其实也就是把条件反过来，然后对调一下`嵌套`的位置而已。

其实大多数教程不怎么讲`if`的`嵌套`，因为是个很正常的思路过程，这里之所以提，是因为`if`的`嵌套`和`循环`的`嵌套`类似。

### 循环的嵌套

循环分两种：`for`和`while`，单纯的循环多少次或者在某个条件成立下循环是很直接的。

例如，循环打印5个“hello”，每个“hello”中间以空格间隔。

先自己思考一下。

> 提示：`print()`函数默认是每调用一次，自动换行一次。
> 
> 用`print('hello', end=" ")`可以实现打印一次不换号，以`" "`空格结尾。

<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>

#### 参考答案

``` python
for i in range(5):
    print('hello', end=" ")
```

打印出来的结果会是：

``` python
hello hello hello hello hello
```

那么，如果我想打印成一个方阵呢？

也就是这样的结果：

``` python
hello hello hello hello hello
hello hello hello hello hello
hello hello hello hello hello
hello hello hello hello hello
hello hello hello hello hello
```

是不是想到了上面讲的`if`的`嵌套`？

那么应该怎么嵌套呢？

可以自己思考思考。

下面又有答案。

> 提示：可以用单纯的`print()`换行

<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>

#### 参考答案

``` python
for i in range(5):
    for i in range(5):
        print('hello', end=" ")
    print()
```

上面就是`for`的`嵌套`，`while`的`嵌套`也是同理。

其实就是在循环体里，再写循环。

可以这样理解，上一节讲的`for`，把一次循环执行称为`迭代`，把它看做普通的若干行代码，只是在若干行代码里，碰上了又一个循环。

或者按照箭头的说法。

1. 第一个`for`箭头指向了第一个`range(5)`的第一个数字`0`。
2. 碰到第二个`for`，就出来另一个箭头，指向第二个`range(5)`的第一个数字`0`，这才执行到内层`for`的循环体，打印一下`hello`。
3. 第二个`for`的第二次迭代，执行了第二个`range(5)`的第二个数字`1`，打印一下`hello`，直到第二个`for`的5次执行完成。
4. 然后碰到`print()`，换行。
5. 第一个`for`的箭头再前进，执行下一次`迭代`，第一个`for`的`range(5)`来到了`1`，再回到`步骤2`。