---
title: Quaternion四元数
date: 2018-10-27 13:44:46
categories:
- Unity
tags:
- Math
- Unity
- GameLogic
---
## 旋转操作

 在unity3d中, quaternion 的乘法操作 (operator  * ) 有两种操作:

1. quaternion *quaternion , 例如 q = t* p; 这是将一个点先进行t 操作旋转,然后进行p操作旋转.
2. Quaternion *Vector3, 例如 p : Vector3, t : Quaternion , q : Quaternion;    q = t* p; 这是将点p 进性t 操作旋转，即对一个向量进行旋转;

Quaternion 的基本数学方程为 :
$$
Q=\cos\frac{angle}{2}+i(x \times \sin \frac{a}{2})+j(y \times \sin \frac{a}{2})+k(z \times \sin \frac{a}{2}) \qquad(a 为旋转角度)\\
\\
Q : Quaternion;\\
Q.w = \cos \frac{angle}{2}\\
Q.x = axis.x \times \sin \frac{angle}{2}\\
Q.y = axis.y \times \sin \frac{angle}{2}\\
Q.z = axis.z \times \sin \frac{angle}{2}
$$

我们只要有角度就可以给出四元数的四个部分值,例如我想要让点M=Vector3(o,p,q) 绕x轴顺时针旋转90度;那么对应的quaternion数值就应该为:
$$
Q : Quaternion;\\
Q.x = 1 \times \sin\frac{90^\circ}{2} = \sin(45^\circ) = 0.7071\\
Q.y = 0\\
Q.z = 0\\
Q.w = cos(90度/2) = cos (45度) = 0.7071\\
Q = \left( 0.7071, 0 , 0 , 0.7071 \right)\\
m = Q \times m\\
\left(将点 m 绕 x轴 \left(1,0,0\right) 顺时针旋转了90度\right)
$$
