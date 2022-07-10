---
title: Marching Square
date: 2018-10-29 03:06:17
categories:
tags:
---
## Marching Squares 是什么

- Marching Squares 是一种平面图形算法，用于生成平面上的图形轮廓。
- 对应的，3D空间中的轮廓生成算法为Marching Cubes，将二维平面的Square，拓展至三维空间的Cube，过程类似但状态更多。

## Marching Squares 原理

- 将平面划分为一个正方形网格，每个网格称作一个Square，也即Wiki上提到的“图素”，每个Square拥有4个控制结点，分别是其四条边的交点，还拥有4个绘制结点，位于每条边中点，且一个控制结点又可被其他Square用作控制结点。（或者说网格上的每4个控制节点组成一个Square）

- 每个控制结点带有权值，并定义一个与结点数组同样规模的布尔数组。（或在类中带有一个布尔值）
- 算法开始时，定义一个阈值，遍历所有控制结点，并且将控制结点的权值与阈值比较，若大于阈值则对应位置的布尔值赋真（或相反）。
- 一个结点在遍历完成后拥有两种状态，0或1，每个Square拥有4个结点，则2<sup>4</sup>=16共有16种状态，而在不同状态下连接对应的两个绘制结点，即完成了一个Square的轮廓生成过程。
- 遍历所有的Square，也即算法名中的Marching，则完成了轮廓的绘制

---

## Wiki上Marching Squares的过程图

![Marching Squares](https://upload.wikimedia.org/wikipedia/commons/thumb/0/00/Marching_squares_algorithm.svg/1065px-Marching_squares_algorithm.svg.png)

---

## 能用来干什么

- 等高线生成
- 我用于2D游戏的简单地形破坏生成（复杂的我不会）
