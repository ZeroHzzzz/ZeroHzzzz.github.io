---
title: Note - 矩阵
date: 2024-05-02 17:12:15
categories:
- Math
---
# 分块矩阵

## 加法
设 $A=\begin{pmatrix}A_{11}&\cdots&A_{1t}\\\vdots&\ddots&\vdots\\A_{s1}&\cdots&A_{st}\end{pmatrix}$，
$B = \begin{pmatrix}B_{11}&\cdots&B_{1t}\\\vdots&\ddots&\vdots\\B_{s1}&\cdots&B_{st}\end{pmatrix}$，则
$$A + B = \begin{pmatrix}A_{11} + B_{11}&\cdots&A_{1t}+B_{1t}\\\vdots&\ddots&\vdots\\A_{s1}+B_{s1}&\cdots&A_{st}+B_{st}\end{pmatrix}$$

## 数乘
设 $A=\begin{pmatrix}A_{11}&\cdots&A_{1t}\\
\vdots&\ddots&\vdots\\A_{s1}&\cdots&A_{st}\end{pmatrix}$，则
$$kA = \begin{pmatrix}kA_{11}&\cdots&kA_{1t}\\\vdots&\ddots&\vdots\\kA_{s1}&\cdots&kA_{st}\end{pmatrix}$$

## 乘法
设 $A=\begin{pmatrix}A_{11}&\cdots&A_{1t}\\
\vdots&\ddots&\vdots\\A_{s1}&\cdots&A_{st}\end{pmatrix}$，$B = \begin{pmatrix}B_{11}&\cdots&B_{1r}\\\vdots&\ddots&\vdots\\B_{t1}&\cdots&B_{tr}\end{pmatrix}$，则
$$AB = \begin{pmatrix}C_{11}&\cdots&C_{1r}\\\vdots&\ddots&\vdots\\C_{s1}&\cdots&C_{sr}\end{pmatrix}$$
其中 $C_{ij}=\sum_{k=1}^tA_{ik}B_{kj}$

## 幂
设 $A = \begin{pmatrix}
A_1 & & & \\
& A_2 & & \\
& & \ddots &\\
& & & A_s
\end{pmatrix}$，则
$$ A^m = \begin{pmatrix}
A_1^m & & &\\
& A_2^m & &\\
& & \ddots &\\
& & & A_s^m\\
\end{pmatrix}$$

## 转置
设 $A=\begin{pmatrix}A_{11}&A_{12}&\cdots&A_{1t}\\A_{21}&A_{22}&\cdots&A_{2t}\\
\vdots&\vdots&\ddots&\vdots\\A_{s1}&A_{s2}&\cdots&A_{st}\end{pmatrix}$，则
$$A' = \begin{pmatrix}A_{11}^\prime&A_{21}^\prime&\cdots&A_{s1}^\prime\\A_{12}^\prime&A_{22}^\prime&\cdots&A_{s2}^\prime\\
\vdots&\vdots&\ddots&\vdots\\A_{1t}^\prime&A_{2t}^\prime&\cdots&A_{st}^\prime\end{pmatrix}$$

## 行列式
$$\begin{vmatrix}
A_{11} &A_{12} &\cdots &A_{1s}\\
0 &A_{22} &\cdots &A_{2s}\\
\vdots &\vdots &\ddots &\vdots\\
0 &0 &\cdots &A_{ss}
\end{vmatrix} = \left\vert A_{11}\right\vert \left\vert A_{22}\right\vert\cdots\left\vert A_{ss}\right\vert$$

$$\begin{vmatrix}
A_{11} & 0 & \cdots & 0\\
A_{21} & A_{22} & \cdots & 0\\
\vdots &\vdots &\ddots &\vdots\\
A_{s1} & A_{s2} & \cdots & A_{ss}
\end{vmatrix} = \left\vert A_{11}\right\vert \left\vert A_{22}\right\vert\cdots\left\vert A_{ss}\right\vert$$

$$\begin{vmatrix}
A_{1} & & & \\
 & A_{2} & & \\
 & & \ddots & \\
 & & & A_{s}
\end{vmatrix} = \left\vert A_{1}\right\vert \left\vert A_{2}\right\vert\cdots\left\vert A_{s}\right\vert$$

## 逆
$$ \begin{pmatrix}
A_1 & & &\\
& A_2 & &\\
& & \ddots &\\
& & &A_s
\end{pmatrix}^{-1} = 
\begin{pmatrix}
A_1^{-1} & & &\\
& A_2^{-1} & &\\
& & \ddots &\\
& & &A_s^{-1}
\end{pmatrix}$$

$$ \begin{pmatrix}
& & &A_1 \\
& & A_2 &\\
&\ddots & &\\
A_s& & &
\end{pmatrix}^{-1} = 
\begin{pmatrix}
 & & &A_s^{-1}\\
 && A_{s-1}^{-1} &\\
& \ddots && \\
A_1^{-1}& & &
\end{pmatrix}$$
# 降阶公式
设 $A$ 为 $m\times n$ 矩阵，$B$ 是 $n\times m$ 矩阵，$m>n$，$\lambda$ 是任意数，则
$$\left\vert\lambda E_m - AB\right\vert = \lambda^{m-n}\left\vert\lambda E_n - BA\right\vert$$

# 矩阵的秩
## 定义
矩阵 $A$ 的非零子式的最高阶数叫作矩阵 $A$ 的秩。

## 性质
设 $A$ 为 $m\times n$ 矩阵，$B$ 为 $n\times p$ 矩阵，则

- $0 \le R(A) \le \min\{m, n\}$
- $R(A') = R(A)$
- $R(kA) = \begin{cases}0&k=0\\R(A)&k\ne0\end{cases}$
- $R(A_1) \le R(A)$，其中 $A_1$ 为 $A$ 的任意一个子矩阵。
- $R\begin{pmatrix}A&0\\0&B\end{pmatrix} = R(A) + R(B)$
- $R\begin{pmatrix}A&C\\0&B\end{pmatrix} \ge R(A) + R(B)$
- $R(A \mid B) \le R(A) + R(B)$
- $R(A + B) \le R(A) + R(B)$
- $R(AB) \le \min\{R(A), R(B)\}$
- $R(AB) \ge R(A) + R(B) - n$
