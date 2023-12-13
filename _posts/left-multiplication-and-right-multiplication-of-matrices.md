---
title: 矩阵左乘和右乘
categories:
  - Math
date: 2023-12-13 18:02:06
---
# 向量乘矩阵
设矩阵A：

$$
A = \begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
$$

设向量x：

$$
x = \begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

那么x右乘矩阵A，我们会得到：

$$
\begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
\begin{bmatrix}
x_{1}\\
x_{2}
\end{bmatrix}
= 
x_1\begin{bmatrix}
a_{11}\\
a_{21}
\end{bmatrix}
+x_2
\begin{bmatrix}
a_{12} \\
a_{22}
\end{bmatrix}
$$

由此可见，上述乘法相对于是对矩阵A中的列向量进行线性组合，线性组合的系数就是x对应位置的元素

那么x左乘矩阵A，我们会得到：

$$
\begin{bmatrix}
x_{1} & x_{2}
\end{bmatrix}
\begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
=
x_1
\begin{bmatrix}
a_{11} & a_{12}
\end{bmatrix}
+x_2
\begin{bmatrix}
a_{21} & a_{22}
\end{bmatrix}
$$

由此可见，向量左乘矩阵A，就相当于对矩阵A中的行向量进行线性组合，线性组合的系数就是向量x上对应位置的元素

# 矩阵乘矩阵

**左乘**，是指将第一个矩阵的列向量作为基，将第二个矩阵的列向量进行线性组合。

**右乘**，是指将第一个矩阵的行向量作为基，将第二个矩阵的行向量进行线性组合。

例如，设矩阵 A 和 B 如下所示：

$$
A=\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
B=\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
$$

则矩阵 A 左乘矩阵 B 的结果如下所示：

$$
C = A \cdot B = \begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix} \cdot \begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix} = \begin{bmatrix}
25 & 22 \\
49 & 42
\end{bmatrix}
$$

矩阵 A 左乘矩阵 B 的结果可以理解为：

* 将矩阵 B 的列向量按顺序排列，得到一个列向量组。
* 将矩阵 A 的每一行向量与列向量组中的每一个向量进行线性组合，得到一个新的列向量。
* 将新的列向量组作为矩阵 C 的列向量。

矩阵 A 右乘矩阵 B 的结果如下所示：

$$
D = B \cdot A = \begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix} \cdot \begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix} = \begin{bmatrix}
53 & 64 \\
95 & 108
\end{bmatrix}
$$

矩阵 A 右乘矩阵 B 的结果可以理解为：

* 将矩阵 A 的行向量按顺序排列，得到一个行向量组。
* 将矩阵 B 的每一行向量与行向量组中的每一个向量进行线性组合，得到一个新的行向量。
* 将新的行向量组作为矩阵 D 的行向量。

# Summary
* 要将矩阵乘法理解称为变换
* 左乘矩阵相当于对原矩阵进行了初等行变换，右乘矩阵相当于对原矩阵进行了初等列变换
* 左乘可以说是矩阵中向量组的变换，而右乘是空间的变换，本质是基向量的改变
