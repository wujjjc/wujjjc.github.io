---
layout: post
title: "SASRec 学习笔记：自注意力序列推荐"
date: 2026-05-31
category: notes
tags: [学习笔记, 推荐系统, SASRec, Transformer, 序列推荐]
---

> SASRec（Self-Attentive Sequential Recommendation）使用多头自注意力机制建模用户交互序列，是序列推荐领域的经典工作。

## 论文信息

- **标题**: Self-Attentive Sequential Recommendation
- **作者**: Kang et al.
- **会议**: ICDM 2018
- **论文链接**: [arXiv:1808.09781](https://arxiv.org/abs/1808.09781)

## 背景与动机

序列推荐的核心目标：根据用户的历史交互序列，预测下一个可能交互的物品。

传统方法的局限：
- **马尔可夫链（FPMC）**：只考虑最近几步交互，丢失长期依赖
- **RNN（GRU4Rec）**：难以并行化，训练速度慢，长序列梯度消失
- **CNN（Caser）**：感受野受限，需要多层堆叠才能捕获长距离关系

SASRec 的出发点：用自注意力机制直接建模序列中任意两个位置之间的依赖关系。

## 模型架构

```
用户交互序列: [i1, i2, i3, ..., it]
        |
   Embedding Layer (物品嵌入 + 位置嵌入)
        |
   Self-Attention Block x N (因果掩码)
        |
   Point-wise Feed-Forward
        |
   输出: 下一时刻物品的概率分布
```

### 输入表示

给定用户交互序列 $s = (s_1, s_2, \ldots, s_t)$，物品嵌入矩阵 $M \in \mathbb{R}^{|\mathcal{V}| \times d}$，序列的嵌入表示为：

$$
E = [e_{s_1}, e_{s_2}, \ldots, e_{s_t}]
$$

加上可学习的位置嵌入 $P \in \mathbb{R}^{t \times d}$：

$$
E' = E + P
$$

### 因果掩码（Causal Mask）

关键设计：位置 $i$ 只能看到位置 $1, 2, \ldots, i$ 的信息，不能看到未来的物品。

在自注意力的 softmax 之前，将未来位置的权重设为 $-\infty$：

$$
\text{mask}(i, j) = \begin{cases} 0 & \text{if } j \leq i \\ -\infty & \text{if } j > i \end{cases}
$$

这保证了模型的自回归特性，训练和推理行为一致。

### 多头自注意力

$$
\text{MultiHead}(Q, K, V) = \text{Concat}(\text{head}_1, \ldots, \text{head}_h) W^O
$$

$$
\text{head}_i = \text{Attention}(Q W_i^Q, K W_i^K, V W_i^V)
$$

$$
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}} + \text{mask}\right) V
$$

### 前馈网络

$$
\text{FFN}(x) = \text{ReLU}(x W_1 + b_1) W_2 + b_2
$$

每个子层（注意力 / FFN）都带有残差连接和层归一化：

$$
\text{LayerNorm}(x + \text{Sublayer}(x))
$$

### 输出预测

取最后一个位置的隐藏状态 $h_t^{(N)}$，与所有物品嵌入做内积：

$$
P(y = i | s) = \frac{\exp(h_t^{(N)} \cdot e_i^T)}{\sum_{j \in \mathcal{V}} \exp(h_t^{(N)} \cdot e_j^T)}
$$

## 训练细节

### 损失函数

使用交叉熵损失，对序列中每个位置做预测：

$$
\mathcal{L} = -\frac{1}{|\mathcal{S}|} \sum_{s \in \mathcal{S}} \sum_{t=1}^{|s|-1} \log P(s_{t+1} | s_1, \ldots, s_t)
$$



### 关键观察

1. **长序列建模能力**：相比 FPMC（只看前一步），SASRec 能利用更长的历史信息
2. **效率优势**：相比 GRU4Rec，自注意力可以并行计算，训练速度快
3. **注意力头数**：1 个头就足够了（ML 1M 数据集上），多头反而可能过拟合

## 个人理解

### 核心思想

SASRec 的本质是把 Transformer 的解码器部分（因果自注意力）应用到序列推荐中。它不编码序列顺序，而是通过位置嵌入隐式学习。

### 与 Transformer 的区别

- **没有编码器**：SASRec 只用解码器侧的因果注意力，因为任务是自回归预测
- **没有交叉注意力**：不需要 encoder-decoder attention，因为没有额外的输入序列
- **嵌入层**：用物品 ID 的嵌入，而非 NLP 中的 token 嵌入

### 局限性

- 只建模了物品序列，没有利用用户特征和上下文信息
- 对冷启动物品无能为力（需要物品有足够多的交互记录）
- 位置嵌入是绝对位置，对不同长度的序列泛化能力有限

## 反思与解答
1. 使用了对比学习，加入可学习的温度系数是否会更好，尝试一下0.07 与 可学习的温度

2. 负采样的大小会带来什么样的直观影响，尝试不同的负采样大小，20，50，100

3. 尝试一下过滤低分样本能否带来效果提升

4. 尝试将用户的性别，年龄，职业编码作为embedding放到序列首位作为全局信息


## 参考资料

1. [原始论文](https://arxiv.org/abs/1808.09781)
2. [SASRec 作者代码 (TensorFlow)](https://github.com/kang205/SASRec)
3. [PyTorch 复现](https://github.com/wujjjc/Sasrec)
