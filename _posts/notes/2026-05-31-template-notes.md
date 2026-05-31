---
layout: post
title: "【模板】学习笔记标题"
date: 2026-05-31
category: notes
tags: [学习笔记, RQ-VAE]
---

> 摘要：一句话概括本篇笔记的内容。

## 基本概念

概念的定义和解释。

## 核心原理

### 要点 1

详细说明。

### 要点 2

详细说明。

## 关键公式

$$
z_q = \arg\min_{z \in \mathcal{C}} \| z_e - z \|^2
$$

## 代码示例

```python
import torch

class VectorQuantizer(torch.nn.Module):
    def __init__(self, num_embeddings, embedding_dim):
        super().__init__()
        self.embedding = torch.nn.Embedding(num_embeddings, embedding_dim)

    def forward(self, z_e):
        # 计算最近邻
        distances = torch.cdist(z_e, self.embedding.weight)
        indices = distances.argmin(dim=-1)
        z_q = self.embedding(indices)
        return z_q, indices
```

## 个人理解

用自己的话总结对这个概念的理解。

## 疑问

- 问题 1
- 问题 2

## 参考资料

1. [资料标题](链接)
