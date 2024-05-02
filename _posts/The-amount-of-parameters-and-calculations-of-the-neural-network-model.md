---
title: 模型参数量和计算量计算
date: 2023-12-10 13:47:34
categories:
  - AI_learning
  - Theories
---
# 基本概念
- FLOPs (Floating-point Operations)
浮点运算次数，理解为计算量，可以用来衡量算法的复杂度。一个乘法或一个加法都是一个FLOPs

- FLOPS(Floating-point Operations Per Second)
每秒浮点运算次数，理解为计算速度，是一个衡量硬件性能的指标

- MACCs(multiply-accumulate operations)
乘-加操作次数，MACCs 大约是 FLOPs 的一半。将$ w * x + b $视为一个乘法累加，也称为1 个 MACC 

- MAC(Memory Access Cost)
内存访问成本

- Params
是指模型训练中需要训练的参数总数

我们可以将参数量理解为空间复杂度，将计算量理解为时间复杂度
# 全连接层
一个全连接权重 W 矩阵为 $ (C_{in}, C_{out}) $， 输入为 $(B,F,C_{in})$,输出$(B,F,C_{out})$(B 代表batch_size, C代表通道数, F代表输入的特征图的大小),则：
$$
Params = (C_{in} + 1 )* C_{out}
$$
$$
FLOPs = (F * C_{in} + 1) * C_{out}
$$
以上计算都很好理解。其中$Params$中$C_{in}$加上1的原因是偏置$b$的存在。如果不懂可以参照这个图：
<center>{%asset_img full-connected-layer.jpg "This is a img..." %}</center>

# 卷积
假设输入特征图为$ (B,C_{in},F) $,卷积核为 k * k ,输出通道为$C_{out}$。
## 参数量
$$
Params = k * k * C_{in} * C_{out}
$$
## 计算量
- 单次卷积操作的乘法次数为$ k * k * C_{in}$, 然后相加，加法次数为$k * k * C_{in} - 1$。这个-1其实就是因为因为在$ k×k×C_{in} -1 $个乘法操作之间，需要$ k×k×C_{in} -1 $次加法操作将它们累加起来。在最后一个乘法操作之后，就不需要再进行一次加法操作了，因此减去1。
- 刚才我们只计算了输出特征图上一个元素的计算量。那么输入特征图上单个通道上的计算量=单个元素的计算量*元素个数，此时我们需要另外一个经典的公式去计算输出特征图大小和输入特征图大小的关系：
$$
n_H = \frac{n_{Hp} - kernel + 2 * pad}{stride} + 1
$$
$$
n_W = \frac{n_{Wp} - kernel + 2 * pad}{stride} + 1
$$
- 然后再考虑通道数，还有偏置，可知计算量
$$FLOPs = (2 * k * k * C_{in} - 1) * (n_H * n_W) * C_{out}(无偏置)$$
$$FLOPs = (2 * k * k * C_{in} - 1 + 1) * n_H * n_W * C_{out}(有偏置)$$
<center>{%asset_img conv_layer.jpg "This is a img..." %}</center>