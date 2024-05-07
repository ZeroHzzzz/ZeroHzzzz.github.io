---
title: 集合与关系
date: 2024-05-07 22:32:06
categories:
---
# 集合的概念与表示
## 集合表示方法
- 列举法：A = {1,2,3,4}
- 描述法：$ B = \left \{  x | x \epsilon A\right \}$

## 包含关系

## 幂集
A的全体子集构成的集合（包括空集）叫做A的幂集,记为$\rho(A) 或者 2^A$
设A = {a,b,c}，则A的幂集为$\rho(A)$ = {$\varnothing  $,{a},{b},{c},{a,b},{a,c},{b,c},{a,b,c}} 

# 集合的运算
## 交运算
$$ A \cap B = \left \{ x | x \in A \wedge  x \in B \right \}$$

## 并运算
$$ A \cup B = \left \{ x | x \in A \vee  x \in B \right \}$$

## 相对补
$$ A - B = \left \{ x | x \in A \wedge  x \notin B \right \}$$

## 绝对补
当相对补中的A为E的时候，记为~B
$$ \sim B = \left \{ x | x \in E \wedge  x \notin B \right \}$$

## 对称差
$$ A \bigoplus  B = \left \{ x | (x \in A \wedge  x \notin B) \vee (x \notin A \wedge  x \in B) \right \}$$

# 包含排斥原理
$ | A \cup B | = |A| + |B| - |A \cap B| $
$ | A \cap B | = |A| + |B| - |A \cup B| $
$ | A \cup B \cup C | = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|$
$ |A₁ ∪ A₂ ∪ ... ∪ Aₙ| = Σ|Aᵢ| - Σ|Aᵢ ⋂ Aⱼ| + Σ|Aᵢ ⋂ Aⱼ ⋂ Aₖ| - ... + (-1)^(n+1) |A₁ ⋂ A₂ ⋂ ... ⋂ Aₙ| $

# 序偶
<a,b>有序的数字组合

# 笛卡尔积
## 定义
$ A \times B = \left \{ <x,y> | x \in A \wedge  y \in B \right \}$

## 运算性质
- $ A \times \varnothing = \varnothing ,\varnothing \times A   = \varnothing$
- 不满足交换律和结合律
- 并和交运算满足分配律

# 关系及其表示
