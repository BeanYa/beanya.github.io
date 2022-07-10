---
mathjax: true
title: Markdown+Latex书写公式
date: 2018-10-31 03:33:20
categories:
- Markdown
tags:
- Note
- Markdown
---



# 在文本中插入公式

## 如何在正文中插入公式?

markdown中使用关键字对`\$ 正文 \$`或者`\$\$ 正文 \$\$` 在文字插入公式.

## 1.在文字的同行中插入公式

在文字同行中插入公式使用关键字对$ 正文 $ (同行插入即不分行)
可能你会问，那怎么输入‘$’ 符号，使用转移字符就可以，即’\$’。

    代码:  我是在文字同行中插入公式: $   f(x)=w^Tx+b $   

我是在文字同行中插入公式: $   f(x)=w^Tx+b $

    代码:  我是在文字中插入\$: $$ 我是  f(\$)=\$^Tx+b $$   

我是在文字中插入$ : $$  f(\$)=\$^Tx+b  $$

(以上不起另一行，但用\$不起效果，用\$\$解决)

## 2. 插入公式另起一行

    代码:  我是在新的一行中插入公式: $$   f(x)=w^Tx+b $$

我是在新的一行中插入公式: $$  f(x)=w^Tx+b  $$

---

# 编辑上标和下标

## 1. 编辑单个上标或者下标

编辑公式使用上标的关键字是`$ ^ $` ，下标是关键字是`$ _ $` .

    代码:  我是在公式中插入上/下标: $   f(x)=w^T_ix_i^2+b_i $

在公式中插入上/下标:$$   f(x)=w^T_ix_i^2+b_i $$

## 2. 编辑双上标或者下标(下/上标为公式)

如果要在公式使用双下/上标或者上/下标插入公式，使用关键字是`$ ^{上标内容} $` ，下标是关键字是`$ _{下标内容} $` 也就是把上/下标的内容包裹到`$ { } $` 内，这个也适用于其他关键字操作.

    代码:  我是在新的一行中插入公式: $$   f(x)=w^{T^t}_{ij}x _{x \in X_i}+b_{ij} $$

在新的一行中插入公式: $$f(x)=w^{T^t}_{ij}x_{x \in X_i}+b_{ij}$$

---

# 编辑特殊符号

## 1. 常见的希腊符号

    代码:  我是在公式中插入希腊符号: $$ f(\alpha)=\beta w^T_i x_i^{\theta}+\mu_i $$

$$   f(\alpha)=\beta w^T_i x_i^{\theta}+\mu_i $$

| 大写希腊符号 | 小写希腊符号 | 大写转义符号 | 小写转移符号 | 大写效果 | 小写效果 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| Α | α |        | \alpha   |           | $ \alpha $    |
| Β | β |        | \beta    |           | $ \beta $     |
| Γ | γ | \Gamma | \gamma   | $\Gamma $ | $ \gamma $    |
| Δ | δ | \Delta | \delta   | $\Delta $ | $ \delta $    |
|   | ε |        | \epsilon |           | $ \epsilon $  |
|   | ζ |        | \zeta    |           | $ \zeta $     |
|   | η |        | \eta     |           | $ \eta $      |
| Θ | θ | \Theta | \theta   | $\Theta $ | $ \theta $    |
|   | ι |        | \iota    |           | $ \iota $     |
|   | κ |        | \kappa   |           | $ \kappa $    |
| ∧ | λ | \Lambda| \lambda  | $\Lambda $| $ \lambda $   |
|   | μ |        | \mu      |           | $ \mu $       |
|   | ν |        | \nu      |           | $ \nu $       |
| Ξ | ξ | \Xi    | \xi      | $\Xi $    | $ \xi $       |
|   | ρ |        | \omicron |           | $ \omicron $  |
| ∏ | π | \Pi    | \pi      | $\Pi $    | $ \pi $       |
|   | ο |        | \rho     |           | $ \rho $      |
| ∑ | σ | \Sigma | \sigma   | $\Sigma $ | $ \sigma $    |
|   | τ |        | \tau     |           | $ \tau $      |
|   | υ |        | \upsilon |           | $ \upsilon $  |
| Φ | φ | \Phi   | \phi     | $\Phi $   | $ \phi $      |
|   | χ |        | \chi     |           | $ \chi $      |
| Ψ | ξ | \Psi   | \psi     | $\Psi $   | $ \psi $      |
| Ω | ξ | \Omega | \omega   | $\Omega $ | $ \omega $    |

## 2. 常见的数学符号

编辑数学符号同样也是通过转义字符来实现的，即$ \ $ ，转移字符配合不同指令即可$ \alpha $ .

    代码:  带数学符号的公式: $$   L(f) = \sum_{i=1}^D(\tilde{y_i}-y_i)^2=\sum_{i=1}^D(wx_i+b-y_i)^2 $$

公式: $$   L(f) = \sum_{i=1}^D(\tilde{y_i}-y_i)^2=\sum_{i=1}^D(wx_i+b-y_i)^2 $$

---

# 常用的数学符号

| 转义符号 | 效果 |
|:---:|:---:|
| \log_{x}y = \arccos z                 | $ \log_{x}y = \arccos z $                 |
| \frac{a} {b}                          | $ \frac{a} {b} $                          |
| _{a}^{b}\textrm{C}                    | $ _{a}^{b}\textrm{C} $                    |
| \frac{\partial {z_x}}{\partial x}     | $ \frac{\partial {z_x}}{\partial x} $     |
| \frac{\partial^2 {x}}{\partial x^2}   | $ \frac{\partial^2 {x}}{\partial x^2} $   |
| \frac{\mathrm{d} y}{\mathrm{d} x}     | $ \frac{\mathrm{d} y}{\mathrm{d} x} $     |
| \int x                                | $ \int x $                                |
| \int_{a}^{b}x                         | $ \int_{a}^{b}x $                         |
| \oint a                               | $ \oint a $                               |
| \oint_{a}^{b}C                        | $ \oint_{a}^{b}C $                        |
| \iint_{a}^{v}C                        | $ \iint_{a}^{v}C $                        |
| \bigcap A                             | $ \bigcap A $                             |
| \bigcap_{a}^{b}C                      | $ \bigcap_{a}^{b}C $                      |
| \bigcup c                             | $ \bigcup c $                             |
| \lim_{c}X                             | $ \lim_{c}X $                             |
| \sum a                                | $ \sum a $                                |
| \sum_{a}^{b}C                         | $ \sum_{a}^{b}C $                         |
| \sqrt{X}                              | $ \sqrt{X} $                              |
| \sqrt[a]{X}                           | $ \sqrt[a]{X} $                           |
| \prod X                               | $ \prod X $                               |
| \prod_{a}^{b} X                       | $ \prod_{a}^{b} X $                       |
| \coprod X                             | $ \coprod X $                             |
| \coprod_{a}^{b} X                     | $ \coprod_{a}^{b} X $                     |
| \left [ a \right ]                    | $ \left [ a \right ]  $                   |
| \left ( a\right )                     | $ \left ( a\right )  $                    |
| \left { a \right }                    | $$ \left\{ a \right\} $$                  |
| \left&#124; a \right&#124;            | $ \left&#124; a \right&#124; $            |
| \left \langle a \right \rangle        | $ \left \langle a \right \rangle $        |
| \left \lfloor a \right \rfloor        | $ \left \lfloor a \right \rfloor $        |
| \left \lceil a \right \rceil          | $ \left \lceil a \right \rceil $          |
| \in A                                 | $ \in A $                                 |
| \supseteqq A                          | $ \supseteqq A $                          |
| \approx                               | $ \approx $                               |
| \sum\limits_{i=1}^{\infty}            | $ \sum\limits_{i=1}^{\infty} $            |

# 可视化编辑器

[可视化编辑器](https://latex.codecogs.com/eqneditor/editor.php)

<iframe src="https://latex.codecogs.com/eqneditor/editor.php" height="500" width="100%">
