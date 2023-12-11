---
title: 反向传播优化器总结（The Summary of Backpropagation Optimizer）
date: 2023-12-10 20:03:10
categories:
    - AI_learning
    - Math
published : false
---
# Beginings
梯度下降算法（Gradient Descent Optimization）是神经网络模型训练最常用的优化算法。对于深度学习模型，基本都是采用梯度下降算法来进行优化训练的。~~其原理也很简单，就是求导（），将其推广到高维空间就是求偏导~~

目标函数$J(\theta)$关于参数$\theta$的梯度就是损失函数（loss function）上升最快的方向，那么同样道理，梯度的反方向指向的就是损失函数下降最快的方向。根据这一特点，我们可以写出网络中每个参数的更新方程
$$
\theta_j = \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta)
$$
$\alpha$ 表示学习率（learning rate）,这个参数设置的目的就是为了走太大~~扯到蛋~~的，或者就是说防止在接近最低点的位置反复横跳
# 梯度下降的三种形式
## BGD(批量梯度下降)
## SGD(随机梯度下降)
## MBGD(小批量梯度下降)
