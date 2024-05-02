---
title: 常用损失函数及一些Notes
categories:
  - AI_learning
  - Theories
date: 2023-12-12 00:53:47
tags:
---

# Begining
很久很久以前，机器学习主要有两大任务：分类和回归任务......


# 基本概念（Note）
- 损失函数：就是用来更新参数的衡量指标
- 风险函数：就是train过程中的loss，用于衡量样本点平均意义下的好坏。注意要除以batch_size
- 泛化函数：就是test过程中的loss


# 回归 (Regression)
在回归任务中，预测值和实际值都是实数，一般采用残差$ y−f(x) $来度量两者的不一致程度

## 均方误差（MSE）/L2损失
说白了就是预测值和实际观测值间差的平方的均值。它只考虑误差的平均大小，不考虑其方向。
$$
MSE = \frac{1}{2n} \sum (y_i - \hat{y_i})^2
$$
特性：
- 经过平方，与真实值偏离较多的预测值会受到更为严重的惩罚,所以不够robust()
- 容易算梯度......

## 均方根误差（root mean suqare error,RMSE）
没错，跟刚刚那个很像，就是多了个根号()
$$
RMSE = \sqrt {\frac{ \sum (y_i - \hat{y_i})^2}{n}}
$$
这个玩意和刚刚那个的区别就是惩罚变轻了

## 平均绝对误差MAE/L1损失
不考虑方向
$$
MAE = \frac{ \sum_{i=1}^{n} \left | y_i - \hat{y_i} \right |}{n}
$$
特性：
- 梯度的计算有点烦，需要用到线性规划
- 异常值的反应更小
- 梯度一直很大，会遗漏最小值

## 平均偏差误差（Mean Bias Error）(不常见)
注意，这里正负误差可以互相抵消，因为他相比MAE来说没有用绝对值。可以确定模型存在正偏差还是负偏差
$$
MBE = \frac{ \sum_{i=1}^{n} (y_i - \hat{y_i})}{n}
$$

## 平均绝对百分比误差（Mean Absolute Pencent Error，MAPE）
相比 RMSE，MAPE 相当于把每个点的误差进行了归一化, 降低了个别离群点带来的绝对误差的影响
$$
MAPE = \sum_{i=1}^{n} \left |\frac{y_i - \hat{y_i}}{y_i} \right | * \frac{100}{n}
$$

## Huber函数
$$
L_{Huber}(f,y) = 
\begin{cases}
(f-y)^2, & \left | f - y \right|  \leqslant \xi\\
2\xi\left | f - y \right| - \xi^2, &\left | f - y \right| > \xi
\end{cases}
$$

这样一来，$\xi$ ~ 0时，Huber趋近于MAE；$\xi$ ~ $\infty$ ， Huber趋近于MSE

但是他需要训练$\xi$这个超参数......

# 分类(Classification)
## 0-1损失函数（zero-one loss）——Perception
就是预测值和目标值不相等为1， 否则为0。我们经常可以在感知机模型里面看到他，属于非凸函数，一般来说也就只能在感知机模型里面看到他
$$
L(Y,f(x)) = 
\begin{cases}
\ 1, &Y \neq f(x) \\
\ 0, &Y = f(x)
\end{cases}
$$

## Logistic损失函数
Logistic损失函数是0-1损失函数的另一个代理损失函数，它也是0-1损失函数的凸上界，且该函数处处光滑。但是该损失函数对所有样本点都惩罚，因此对异常值更加敏感。当预测值$f \epsilon = [-1, 1]$时，另一个常用的代理损失函数是交叉熵损失函数
$$
L(f,y) = \log_2(1+\exp(-fy))
$$

## 对数损失函数（log）——LR
~~这里懒得手写LaTeX公式了()，直接用图片说明：~~
<center>{%asset_img log.png This is a photos...%}</center>

## Cross-Entropy(交叉熵)损失函数
交叉熵损失函数也是0-1损失函数的光滑凸上界
$$
L(f,y) = \log_2(\frac{1+fy}{2})
$$

## Exponential(指数)损失函数(AdaBoost)
指数损失函数是AdaBoost里使用的损失函数，同样地，它对异常点较为敏感，缺乏rebust
$$
L(f,y) = e^{-fy}
$$
