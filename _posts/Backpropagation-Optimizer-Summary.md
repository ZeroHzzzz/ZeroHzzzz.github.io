---
title: 反向传播优化器总结（The Summary of Backpropagation Optimizer）
date: 2023-12-12 2:21:10
categories:
    - AI_learning
    - Theories
---
# Beginings
梯度下降算法（Gradient Descent Optimization）是神经网络模型训练最常用的优化算法。对于深度学习模型，基本都是采用梯度下降算法来进行优化训练的。~~其原理也很简单，就是求导（），将其推广到高维空间就是求偏导~~

目标函数$J(\theta)$关于参数$\theta$的梯度就是损失函数（loss function）上升最快的方向，那么同样道理，梯度的反方向指向的就是损失函数下降最快的方向。根据这一特点，我们可以写出网络中每个参数的更新方程
$$
\theta_j = \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta)
$$
$\alpha$ 表示学习率（learning rate）,这个参数设置的目的就是为了走太大~~扯到蛋~~的，或者就是说防止在接近最低点的位置反复横跳
# 梯度下降的三种基本形式
其实说到底只有BGD是最基本的，SGD和MBGD其实都是对BGD的优化。但是看在也是很基础的份上我就把他归于基本的梯度下降方式
## BGD(批量梯度下降)
BGD使用整个训练数据集来计算每一步的梯度。具体来说，它计算损失函数对所有样本的梯度，然后根据该梯度来更新模型参数。但这意味着在每一次迭代中，都要考虑整个数据集，所以计算速度非常慢，无法进行在线学习，即便可以，一个样本加入到大数据集中，对梯度影响也不明显。唯一的优点就是~~容易写~~它对整个数据集进行了全局考虑，因此可以更准确地朝着最优参数的方向前进

它对于凸函数可以收敛到全局极小值，对于非凸函数可以收敛到局部极小值。

如果用X代表数据集，那么他的更新规则是：
$$
\nabla L(X;\theta_l) = \frac{1}{m} \sum_{x_i \epsilon X} \nabla l(x_i;\theta_l)
$$
$$
\theta_{l+1} = \theta_{l} - \alpha \nabla L(X;\theta_l)
$$

## SGD(随机梯度下降)
说白了就是在BGD的基础上，每次迭代仅使用一个随机样本来计算梯度和更新模型参数。这也导致了他容易受数据集中一些异常值的影响，导致更新过程不稳定。但是也恰恰是整个不稳定的特性让他有时可以更容易的跳出梯度高原().....这也可以提高计算速度和内存效率。由于每次只使用一个样本，SGD的计算开销较小，特别适用于大型数据集

更新规则是：
$$
\theta_{l+1} = \theta_{l} - \alpha \nabla l(x_i;\theta_l)
$$
其中$\nabla l(X;\theta_l)$ 是损失函数关于单个样本$x_i$的梯度

SGD 虽然能达到极小值，但是比其它算法用的时间长，而且可能会被困在鞍点。

如果需要更快的收敛，或者是训练更深更复杂的神经网络，需要用一种自适应的算法。

## MBGD(小批量梯度下降)
从这个标题出现的位置和他的命名我们就可以大概的猜出来，这个玩意介于BGD和SGD之间，集合了两家之长，降低了更新时的方差，收敛更加稳定。

MBGD每次迭代时不是使用整个数据集，也不是只使用单个样本，而是使用一个小批量样本。这个小批量的大小通常是一个可调节的超参数，也就是batch_size

其更新规则是：
$$
\theta_{l+1} = \theta_{l} - \alpha \nabla (\frac{1}{b}\sum_{i=1}^b l(x_i;\theta_l))
$$

# 梯度下降法的优化
## 动量优化算法（Momentum）
它引入了动量项v，它是之前梯度的加权平均，模拟了物体在运动中的积累速度的效果，从而帮助跨越局部最小值并更快地收敛到全局最小值。

动量项有助于平滑更新过程，减少参数更新的方差，特别是在存在高曲率或噪声的情况下。它还有助于加速梯度下降，特别是在平原上的方向。同时，动量的积累效果有助于在参数空间中跨越局部最小值，因为动量使得更新在原有方向上继续前进。特别适用于复杂的损失函数和参数空间中存在局部极小值的情况。

对于给定的模型参数$\theta$，动量项v的更新规则如下：

$$
v_{l+1} = \beta v_t + (1 - \beta) \nabla L(\theta_l)
$$
$\beta$ 是动量参数，通常取一个介于0到1之间的值

相应的，其参数的更新规则为：
$$
\theta_{l+1} = \theta_{l} - \alpha v_{l+1}
$$

## Nesterov Accelerated Gradient（NAG）
这是对动量算法的改进。NAG 在更新参数时先根据当前动量位置预估下一步的位置，然后计算梯度进行更新。
NAG首先根据当前动量位置$v_t$预估下一步的位置。预估的下一步位置为$\theta_l - \beta v_t$，其中$\beta$是动量参数。其主要优势在于它对动量的使用进行了改进，提供更准确的预估位置，有助于在参数更新时更精确地调整方向。这使得 NAG 在一些情况下比标准动量算法表现更好

参数更新规则为：
$$
\theta_{l+1} = \theta_{l} - \alpha \nabla_\theta L(\theta_l - \beta v_l)
$$
$$
v_{l+1} = \beta v_l + \alpha \nabla_\theta L(\theta_l - \beta v_l)
$$

## Adagrad （Adaptive gradient algorithm）
很牛逼的一个东西，自适应学习率。它根据每个参数的历史梯度信息自适应地调整学习率，使得对于稀疏梯度的参数可以具有更大的学习率，而对于频繁出现的参数可以有较小的学习率。适用于稀疏数据和非平稳目标函数，但它可能在训练后期过于减小学习率，导致更新步长过小，难以收敛。因此出现了后面的RMSprop和Adam。但是，RMSprop, Adadelta, Adam 在很多情况下的效果其实是相似的。

参数更新规则如下：
$$
\theta_{l+1} = \theta_l - \frac{\alpha}{\sqrt{G_l + \epsilon}} \cdot \nabla_{\theta} L(\theta_l)
$$
其中$G_l$是历史梯度平方的累积，$\epsilon$是一个小的常数用于数值稳定性

## Adadelta
Adadelta 是是 Adagrad 的一种改进版本，解决了 Adagrad 在训练后期学习率过小的问题，不需要手动设置初始学习率，并且对学习率进行了更加平滑和自适应的调整。它使用了对梯度平方的滑动平均，而不是历史梯度平方的累积。这解决了 Adagrad 学习率过早减小的问题。适用于处理非平稳目标函数和具有不同尺度的参数的情况。

参数更新规则：
$$
\theta_{l+1} = \theta_l - \frac{\sqrt{E[g^2]_t + \epsilon}}{\sqrt{E[\Delta \theta^2]l + \epsilon}}  \nabla_{\theta} L(\theta_l)
$$

其中，$ \nabla_{\theta} L(\theta_l) $ 是损失函数关于参数 $ \theta $ 的梯度，$ E[g^2]_l $是梯度平方的滑动平均，$ E[\Delta \theta^2]l $是参数更新的滑动平均

## RMSprop
RMSprop是对 Adagrad 的改进，通过引入衰减系数来减轻学习率的过早减小问题。使用滑动平均来累积梯度平方，这有助于自适应地调整学习率，对于稀疏梯度和非平稳目标函数效果较好。引入了一个衰减系数ρ，它控制了滑动平均的速度。通常ρ取值为接近于1的数，如0.9。适用于处理非平稳目标函数和具有不同尺度的参数的情况

参数更新规则：
$$
\theta_{l+1} = \theta_l - \frac{\alpha}{ \sqrt{E[g^2]_t + \epsilon}} \nabla_{ \theta} L( \theta_t)
$$
## Adam：Adaptive Moment Estimation
Adam结合了动量（momentum）和 RMSprop 的思想，引入了动量项，用$m_l$表示，同时引入了RMSprop的思想，使用了梯度平方的滑动平均，用$v_l$表示。随着梯度变的稀疏，Adam 比 RMSprop 效果更好。

参数更新规则：
$$
\theta_{t+1} = \theta_t - \frac{\alpha \cdot m_t}{\sqrt{v_t} + \epsilon}
$$
$$
m_{t+1} = \beta_1 \cdot m_t + (1 - \beta_1) \cdot \nabla_{\theta} L(\theta_t)
$$
$$
v_{t+1} = \beta_2 \cdot v_t + (1 - \beta_2) \cdot (\nabla_{\theta} L(\theta_t))^2
$$
其中$\beta_1 和 \beta_2$都是衰减系数，通常取接近于1的数

整体来讲，Adam 是最好的选择。