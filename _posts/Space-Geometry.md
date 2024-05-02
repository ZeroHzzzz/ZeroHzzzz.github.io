---
title: Note - 空间几何
date: 2024-05-02 17:17:25
categories:
- Math
---
# 向量
## 数量积
### 定义
设 $a, b$ 是两个几何向量，称 $\left\vert a\right\vert \left\vert b\right\vert \cos\theta$ 为 $a$ 与 $b$ 的**数量积**或**内积**，记作 $a \cdot b$，即
$$a \cdot b = \left\vert a\right\vert \left\vert b\right\vert \cos\theta$$

### 性质
- $a \cdot b = b \cdot a$（交换律）
- $(ka) \cdot b = k(a \cdot b)$
- $(a + b) \cdot c = a \cdot c + b \cdot c$（分配律）
- $a \cdot a \ge 0$。此外，$a \cdot a = 0$ 的充要条件是 $a = 0$。

## 向量积
### 定义
若 $a, b$ 不平行，则
- $\left\vert a \times b\right\vert = \left\vert a\right\vert \left\vert b\right\vert \sin\theta$
- $a \times b \perp a, a \times b \perp b$
- 向量 $a, b, a \times b$ 构成右手系

### 性质
- $a \times b = -b \times a$
- $(ka)\times b = k(a\times b) = a \times (kb)$
- $(a + b) \times c = (a \times c) + (b \times c)\\a \times (b + c) = (a \times b) + (a \times c)$

## 混合积
### 定义
已知三个向量 $a, b$ 和 $c$。先作 $a$ 和 $b$ 的向量积 $a \times b$，把所得的向量与 $c$ 再作数量积 $(a \times b) \cdot c$，这样得到的数量叫做三向量 $a, b, c$ 的**混合积**，记为 $\left[abc\right]$。

向量的混合积有如下几何意义：$\left[abc\right] = (a \times b) \cdot c$ 的绝对值表示以向量 $a, b, c$ 为棱的平行六面体的体积。如果向量 $a, b, c$ 组成右手系，那么混合积的符号是正的；如果 $a, b, c$ 组成左手系，那么混合积的符号是负的。

### 性质
$$ \left[abc\right] = 0 \Leftrightarrow a,b,c\ 共面$$
$$\left[abc\right] = \left[bca\right] = \left[cab\right] = -\left[bac\right] = -\left[cba\right] = -\left[acb\right]$$
设 $a = (a_x, a_y, a_z), b = (b_x, b_y, b_z), c = (c_x, c_y, c_z)$，则
$$
[abc] = 
\begin{vmatrix}
a_x & a_y & a_z \\
b_x & b_y & b_z \\
c_x & c_y & c_z
\end{vmatrix}
$$
# 空间中的平面与直线

## 平面
设平面 $\pi$ 通过点 $M_0(x_0, y_0, z_0)$ 并且垂直于非零向量 $n = (A, B, C)$，则平面 $\pi$ 的**点法式方程**为：
$$A(x - x_0) + B(y - y_0) + C(z - z_0) = 0$$
将其整理得
$$Ax + By + Cz + D = 0$$
其中 $D = -(Ax_0 + By_0 + Cz_0)$，称其为平面 $\pi$ 的**一般方程**

设 $M_1(x_1, y_1, z_1), M_2(x_2, y_2, z_2), M_3(x_3, y_3, z_3)$ 是空间中不在同一条直线上的三点，则称
$$\begin{vmatrix}
x - x_1 & y - y_1 & z - z_1\\
x_2 - x_1 & y_2 - y_1 & z_2 - z_1\\
x_3 - x_1 & y_3 - y_1 & z_3 - z_1
\end{vmatrix}
= 0$$
为平面 $\pi$ 的**三点式方程**。

设平面 $\pi$ 与 $x, y, z$ 轴分别交于 $P(a, 0, 0), Q(0, b, 0), R(0, 0, c)$，则称
$$\frac{x}{a} + \frac{y}{b} + \frac{z}{c} = 1$$
为平面 $\pi$ 的**截距式方程**。

## 直线
设直线 $L$ 过点 $M_0(x_0, y_0, z_0)$，并且平行于已知非零向量 $s = (m, n, p)$，则称
$$\frac{x - x_0}{m} = \frac{y - y_0}{n} = \frac{z - z_0}{p}$$
为直线 $L$ 的**标准方程**。

令其比值为 $t$，则称
$$\begin{cases}
x = x_0 + mt \\
y = y_0 + nt \\
z = z_0 + pt
\end{cases}$$
为直线 $L$ 的**参数方程**。

设平面 $\pi_1, \pi_2$ 为
$$\pi_1 : A_1x + B_1y + C_1z + D_1 = 0\\
\pi_2 : A_2x + B_2y + C_2z + D_2 = 0$$
若 $\pi_1, \pi_2$ 的交线为直线 $L$，则称
$$\begin{cases}
A_1x + B_1y + C_1z + D_1 = 0\\
A_2x + B_2y + C_2z + D_2 = 0
\end{cases}$$
为直线 $L$ 的**一般方程**。

设直线 $L$ 过点 $M_0(x_0, y_0, z_0)$ 和点 $M_1(x_1, y_1, z_1)$，则称
$$\frac{x - x_0}{x_1 - x_0} = \frac{y - y_0}{y_1 - y_0} = \frac{z - z_0}{z_1 - z_0}$$
为直线 $L$ 的**二点式方程**。

# 位置关系
## 平面与平面

设有两个平面
$$
\pi_1 : A_1x + B_1y + C_1z + D_1 = 0 \\
\pi_2 : A_2x + B_2y + C_2z + D_2 = 0
$$
可将 $\pi_1, \pi_2$ 的位置关系分为如下三种情形。

1. $\pi_1, \pi_2$ 重合。其充要条件是
$$
\frac{A_1}{A_2} = \frac{B_1}{B_2} = \frac{C_1}{C_2} = \frac{D_1}{D_2}
$$
2. $\pi_1, \pi_2$ 平行（不包括重合）。其充要条件是
$$
\frac{A_1}{A_2} = \frac{B_1}{B_2} = \frac{C_1}{C_2} \ne \frac{D_1}{D_2}
$$
3. $\pi_1, \pi_2$ 交于一条直线。其充要条件是 $n_1 = (A_1, B_1, C_1)$ 与 $n_2 = (A_2, B_2, C_2)$ 不平行。

当 $\pi_1, \pi_2$ 是两个相交的平面时，称它们的法向量的夹角 $\varphi$ 为这两个平面的夹角，通常规定
$$0 \le \varphi \le \frac{\pi}{2}$$
平面 $\pi_1$ 与 $\pi_2$ 的夹角 $\varphi$ 可由公式
$$
\cos\varphi = \frac{\left\vert A_1A_2 + B_1B_2 + C_1C_2 \right\vert}{\sqrt{A_1^2 + B_1^2 + C_1^2}\sqrt{A_2^2 + B_2^2 + C_2^2}}
$$
来确定。

显然，$\pi_1$ 与 $\pi_2$ 垂直的充要条件时它们的法向量 $n_1$ 与 $n_2$ 垂直，即
$$A_1A_2 + B_1B_2 + C_1C_2 = 0$$

## 直线与直线
设有两条直线
$$
L_1 : \frac{x - x_1}{m_1} = \frac{y - y_1}{n_1} = \frac{z - z_1}{p_1}\\
L_2 : \frac{x - x_2}{m_2} = \frac{y - y_2}{n_2} = \frac{z - z_2}{p_2}
$$
$M_1(x_1, y_1, z_1), M_2(x_2, y_2, z_2)$ 分别是 $L_1, L_2$ 上的定点。$s_1=(m_1, n_1, p_1), s_2=(m_2, n_2, p_2)$ 分别是 $L_1, L_2$ 的方向向量。

可将 $L_1, L_2$ 的位置关系分成如下四种情形
1. $L_1, L_2$ 重合。其充要条件是
$$
\frac{m_1}{m_2} = \frac{n_1}{n_2} = \frac{p_1}{p_2}
$$
且 $M_1 \in L_2 \ (M_2 \in L_1)$，即
$$
\frac{x_1 - x_2}{m_2} = \frac{y_1 - y_2}{n_2} = \frac{z_1 - z_2}{p_2}
$$
2. $L_1, L_2$ 平行（不包括重合）。其充要条件是
$$
\frac{m_1}{m_2} = \frac{n_1}{n_2} = \frac{p_1}{p_2}
$$
且 $M_1 \notin L_2 \ (M_2 \notin L_1)$，即
$$
\frac{x_1 - x_2}{m_2} = \frac{y_1 - y_2}{n_2} = \frac{z_1 - z_2}{p_2}
$$
不成立。

3. $L_1, L_2$ 交于一点。其充要条件是混合积 $\left[s_1s_2\overrightarrow{M_1M_2}\right] = 0$ 且 $s_1s_2$ 不平行。

4. $L_1, L_2$ 是异面直线。其充要条件是混合积 $\left[s_1s_2\overrightarrow{M_1M_2}\right] \ne 0$。

我们规定 $L_1, L_2$ 的方向向量 $s_1, s_2$ 的夹角 $\varphi$ 为这两条直线的夹角。通常规定 $0 \le \varphi \le \frac{\pi}{2}$。

直线 $L_1, L_2$ 的夹角 $\varphi$ 可由公式
$$
\cos\varphi = \frac{\left\vert s_1 \cdot s_2\right\vert}{\left\vert s_1\right\vert \left\vert s_2 \right\vert} 
$$
来确定。

显然，$L_1$ 与 $L_2$ 垂直的充要条件是 $s_1$ 与 $s_2$ 垂直，即
$$
s_1 \cdot s_2 = m_1m_2 + n_1n_2 + p_1p_2 = 0
$$

## 直线与平面
设有一条直线
$$
L : \frac{x - x_0}{m} = \frac{y - y_0}{n} = \frac{z - z_0}{p}
$$
及一个平面
$$
\pi : Ax + By + Cz + D = 0
$$
可将 $L, \pi$ 的位置关系分成如下三种情形。
1. $L$ 在 $\pi$ 上。其充要条件是 $s = (m, n, p)$ 与 $n = (A, B, C)$ 垂直，且 $M_0 \in \pi$，即
$$
\begin{cases}
mA + nB + pC = 0\\
Ax_0 + By_0 + Cz_0 + D = 0
\end{cases}
$$
2. $L$ 与 $\pi$ 平行（不包括 $L$ 在 $\pi$ 上的情形）。其充要条件是 $s = (m, n, p)$ 与 $n = (A, B, C)$ 垂直，且 $M_0 \notin \pi$，即
$$mA + nB + pC = 0$$
且
$$Ax_0 + By_0 + Cz_0 + D \ne 0$$
3. $L$ 与 $\pi$ 交于一点。其充要条件是 $s = (m, n, p)$ 与 $n = (A, B, C)$ 不垂直，即
$$mA + nB + pC \ne 0$$
直线 $L$ 与其在平面 $\pi$ 上的投影直线 $L_1$ 的夹角 $\varphi$ 称为**直线 $L$ 与平面 $\pi$ 的夹角**，通常规定 $0 \le \varphi \le \frac{\pi}{2}$。

$\varphi$ 可由公式
$$
\sin\varphi = \frac{\left\vert s \cdot n \right\vert}{\left\vert s \right\vert \left\vert n \right\vert}
$$
确定。显然，$L$ 与 $\pi$ 垂直的充要条件是 $n$ 与 $s$ 平行，即
$$
\frac{A}{m} = \frac{B}{n} = \frac{C}{p}
$$

# 距离
## 点到平面
设 $M_0(x_0, y_0, z_0)$ 是平面 $\pi : Ax + By + Cz + D = 0$ 外一点。在平面 $\pi$ 上任取一点 $M_1(x_1, y_1, z_1)$，取平面 $\pi$ 的法向量 $n = (A, B, C)$，则点 $M_0$ 到平面 $\pi$ 的距离 $d$ 为
$$d = \frac{\left\vert n \cdot \overrightarrow{M_0M_1} \right\vert}{\left\vert n \right\vert} $$

## 两平行平面
可以转化为点到平面间的距离

## 直线到其平行的平面
可以转化为点到平面间的距离

## 点到直线
设直线 $L$ 的标准方程为
$$
L : \frac{x - x_0}{m} = \frac{y - y_0}{n} = \frac{z - z_0}{p}
$$
即 $L$ 过点 $M_0(x_0, y_0, z_0)$，并且方向向量为 $s = (m, n, p)$。再设 $M_1(x_1, y_1, z_1)$ 是直线 $L$ 外一点，则点 $M_1$ 到直线 $L$ 的距离 $d$ 为
$$
d = \frac{\left\vert s \times \overrightarrow{M_0M_1}\right\vert}{\left\vert s\right\vert}
$$

## 两平行直线
可以转化为点到直线间的距离

## 两异面直线
设由两条异面直线：
$$
L_1 : \frac{x - x_1}{m_1} = \frac{y - y_1}{n_1} = \frac{z - z_1}{p_1}\\
L_2 : \frac{x - x_2}{m_2} = \frac{y - y_2}{n_2} = \frac{z - z_2}{p_2}
$$
记 $P_1(x_1, y_1, z_1), P_2(x_2, y_2, z_2)$ 分别是 $L_1, L_2$ 上的点。$L_1, L_2$ 的方向向量 $s_1 = (m_1, n_1, p_1)$，$s_2 = (m_2, n_2, p_2)$ 分别与 $L_1, L_2$ 的公垂线垂直，所以 $s_1 \times s_2$ 是 $L_1, L_2$ 的公垂线的方向向量。

$\overrightarrow{P_1P_2}$ 在 $s_1 \times s_2$ 上的投影的绝对值就是 $L_1$ 与 $L_2$ 之间的距离 $d$，即
$$
d = \left\vert \overrightarrow{P_1P_2} \cdot \frac{s_1 \times s_2}{\left\vert s_1 \times s_2 \right\vert} \right\vert
$$

# 平面束
称通过给定直线 $L$ 的所有平面的全体为通过直线 $L$ 的**平面束**。

设 $L$ 的一般方程为
$$
\begin{cases}
A_1x + B_1y + C_1z + D_1 = 0\\
A_2x + B_2y + C_2z + D_2 = 0
\end{cases}
$$
其中系数 $A_1, B_1, C_1$ 与 $A_2, B_2, C_2$ 不成比例。则称方程
$$
A_1x + B_1y + C_1z + D_1 + \lambda(A_2x + B_2y + C_2z + D_2) = 0
$$
为通过直线 $L$ 的**平面束方程**。