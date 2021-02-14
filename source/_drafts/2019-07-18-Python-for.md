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

在讲`for`之前，需要知道`数组`或者`列表`的概念。

### 列表

列表其实就是一些变量的有序组合，注意，是`有序`组合。至于为什么强调有序，看到`set`等其他数据类型时就能明白。

假设现在，你需要存储50个同学的数学成绩，在没有`列表`以前，你需要这样做：

``` python
math1 = 0
math2 = 0
math3 = 0 
math4 = 0
math5 = 0
...
...
...
math50 = 0
```

声明50个变量，并且一一赋值。这是很笨的方法，并且效率很低。

那么，思考一下，是否为上面这些变量每一个单独命名是没有意义的呢？

`列表`就派上用场了。只要简单声明，就能使用一个列表：

``` python
math = []
```

或

``` python
math = list()
```

不同的是，这个列表一开始并没有限定大小，它可以存储若干个数据。

需要往列表里面添加数据，用函数`math.append()`。

例如我想向列表里面添加1个数字`0`，那么就是：

``` python
math.append(0)
```

并且，列表是可以被直接`print()`函数打印的。

``` python
math = []
math.append(0)
math.append(1)
print(math)
```

可以得到结果

``` python
[0, 1]
```

中括号表示这是一个`列表`变量，每个元素以`,`分隔开。

`列表`也是一个变量，变量名就代表了一整个`列表`，如果要访问，或者叫做获取列表里某一个元素的话怎么办呢？

就需要用到下标，就像数学里头数列的累加公式里，`ai`是有下标的。

下标表示，元素在`列表`中的位置，下标从`0`开始，访特定位置的`列表`元素，用`列表变量名[下标]`的方式访问。

也就是说，如果现在有一个列表，存储了一组数学成绩：

``` python
math = [10, 20, 90, 40, 30]
```

可以看出来，这个`列表`一共包含`5`个数字，下标从`0`开始。

而`0->4`一共5个数字，也就是`4`是`列表`下标的最大值，`0`是最小值

每一个元素的访问方式如下：

* 10 ---> math[0]
* 20 ---> math[1]
* 90 ---> math[2]
* 40 ---> math[3]
* 30 ---> math[4]

但是，访问`列表`的数据，不能超过列表当前的大小。

比如，现在的`math`只有`5`个元素，下标最大的值是`4`，那么你如果想打印或者使用`math[5]`，那么会告诉你报错了，错误是：` list assignment index out of range`，也就是`列表`下标越界了。

>可以通过`math.append(0)`来向`列表`添加元素，这里的参数`0`是任意的，意思是向`列表`添加元素`0`

那么，像`列表`这一小标题开头举的例子里讲的，现在知道了能用`列表`来存储若干个数字，但是要给他们每一个都赋初始值，比如`10`，是不是还是有点麻烦？

脑海里是不是想：

``` python
math[0] = 10
math[1] = 10
math[2] = 10
...
...
math[49] = 10
```

>注意，0 -> 49 一共50个数。

那么，`for`就派上用场了

### for 在列表例子里的应用

讲完上面的`列表`，为什么要强调有序呢？因为有序，你就可以按顺序的，访问，或者叫做获取每一个数字。

你可以想象有个箭头，从`列表`的第一个元素，每次往前跳一步，一直走到最后一个元素，这个过程叫做`遍历（traverse）`。

而`for`其实就是在对`列表`进行这么一个`遍历`的过程

通过上一节的`函数`和这一节的`列表`，那么`range(10)`这个`函数`其实生成了一个`列表`。

`列表`里面存储了一排从`0`开始，到`range(x)`的`x-1`为止的等差数列，差是`1`。

>其实，`range(x)`并不是真的生成了一个`列表`，他生成的是一个`可迭代对象`，就像箭头一样，这一次需要用到它，他就告诉你是不是走到了`列表`的尾巴，如果不是，就返回这个“箭头”指向的数据，如果到尾了，那么就结束`迭代`。
>
>但是为了降低理解难度，目前先当做是生成了一个`列表`就好了，下面也是这么讲的。

也就是：

``` python 
print(list(range(10)))
```

结果是：

``` python
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

>`range(10)`省略了第一个参数，函数提供了一个默认的参数值，
>
>所以其实`range(10)`是`range(0,10)`，也就是`0-10`范围的整数
>
>这一点如果你直接`print(range(10))`可以得到结果`range(0, 10)`，也就是为什么上面的打印结果我加了一个`list()`，让他转换为`列表`。

那么你就能明白，重复执行50次，不需要重新声明一个变量，再去`while`的条件里面做判断。

例如，对上面的例子的补充，想对50个数学成绩`依次`赋值为`10`，用`for`可以是：

``` python
math = []
for i in range(50):
    math.append(i)
    math[i] = 10
```

因为`列表`不能够访问超过下标的元素，所以需要每次赋值（也就是访问、使用）前，向`列表`添加一个元素，也就是`math.append(i)`的作用

而`i`，其实也就是`遍历`过程中的箭头。

一开始指向`range(50)`生成`列表`的第一个元素`0`，所以`i`的值就是`0`。

下一次的循环里，`i`就是`1`，依次类推，直到最后一次循环，`i`的值是`49`。

当然，上面这么写只是为了告诉你，需要先添加、拓展`列表`，才能访问`列表`的元素。

简单的写法其实就是：

``` python
math = []
for i in range(50):
    math.append(10)
```

## 和while的区别

在python里，`while`和`for`的区别在于，`while`用来广泛的判断`条件`是否成立，再进行循环。

而`for`的作用在于，用来对一个`列表`进行`迭代`或者叫`遍历`。

## 小结

`for`的形式：

``` python
for iterating_var in sequence:
   statements(s)
```

每一次的循环，称作一次`迭代`，所以`iterating_var`代表的是，在这次`迭代`中，当前`列表`也就是`sequence`被指向的值。

可以想象，其实也就是对一个`列表`，用一个箭头，依次的指向`列表`里的值，然后执行循环体，再移动到下一个`列表`的元素。