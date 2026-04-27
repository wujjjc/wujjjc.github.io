---
layout: default
---

<style>
  .project {
    margin-bottom: 2rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid #e1e4e8;
  }
  .project h2 {
    margin-bottom: 0.25rem;
  }
  .project .tech-stack {
    font-size: 0.85rem;
    color: #586069;
    margin-bottom: 0.5rem;
  }
  .project .description {
    margin: 0.5rem 0;
    line-height: 1.5;
  }
  .project .metrics {
    background: #f6f8fa;
    padding: 0.5rem 0.75rem;
    border-radius: 6px;
    font-family: monospace;
    font-size: 0.9rem;
    margin: 0.5rem 0;
  }
  .project .links {
    margin-top: 0.5rem;
  }
  .project .links a {
    margin-right: 1rem;
  }
  hr {
    margin: 1.5rem 0;
  }
</style>

<div style="text-align: right; margin-bottom: 20px;">
  <button id="btn-zh">中文</button> | <button id="btn-en">English</button>
</div>

<!-- ==================== 中文内容 ==================== -->
<div id="zh-content" style="display: block;">

# 欢迎来到我的主页

Hi，我是 wujjjc，一个对推荐系统和深度学习感兴趣的学习者。下面是我的一些项目。

---

## 项目

### 📌 SASRec – 自注意力序列推荐模型

<div class="project">
  <div class="tech-stack">PyTorch | Transformer | 自注意力机制 | 序列建模</div>
  <div class="description">
    基于 PyTorch 完整复现了经典序列推荐模型 SASRec（Self-Attentive Sequential Recommendation），
    采用多头自注意力层代替传统 RNN/CNN 捕获用户交互序列中的长期依赖关系，
    结合位置嵌入和因果掩码保证自回归预测。
  </div>
  <div class="metrics">
    📊 Metrics: Recall@10 = 80% | NDCG@10 = 59% (MovieLens 1M)
  </div>
  <div class="links">
    🔗 <a href="https://github.com/wujjjc/Sasrec">GitHub Repository</a>
  </div>
</div>

### 📌 GemiRec – 兴趣量化与生成的多兴趣推荐系统

<div class="project">
  <div class="tech-stack">PyTorch | GPT | 向量量化 (RQ-VAE) | ANN 检索</div>
  <div class="description">
    提出生成式多兴趣召回框架，通过兴趣量化强制结构化的兴趣分离，通过生成模型显式学习兴趣演化。<br>
    • <strong>IDMM</strong>：采用残差量化编码将物品映射到离散兴趣字典，在结构上保证兴趣分离。<br>
    • <strong>MIPDM</strong>：使用 6 层 GPT 预测用户下一时刻的兴趣分布，推理时通过 Top‑K 兴趣缓存避免延迟。<br>
    • <strong>MIRM</strong>：融合用户嵌入与量化兴趣嵌入进行多兴趣召回。
  </div>
  <div class="metrics">
    📊 Metrics: RetailRocket Recall@20 = 26% | NDCG@20 = 15% 
  </div>
  <div class="links">
    🔗 <a href="https://github.com/wujjjc/GemiRec">GitHub Repository</a>
  </div>
</div>

---

### 🔧 其他项目

- **天池项目**：[alitianchi](https://github.com/wujjjc/alitianchi)

---

### 📖 学习笔记

- [RQ-VAE 笔记](https://www.cnblogs.com/GlenTt/p/19094976)（非本人撰写，仅供学习参考）

---

## 联系

- GitHub: [@wujjjc](https://github.com/wujjjc)

</div>

<!-- ==================== 英文内容 ==================== -->
<div id="en-content" style="display: none;">

# Welcome to My Homepage

Hi, I'm wujjjc, a learner interested in recommender systems and deep learning. Here are some of my projects.

---

## Projects

### 📌 SASRec – Self-Attentive Sequential Recommendation

<div class="project">
  <div class="tech-stack">PyTorch | Transformer | Self-Attention | Sequential Modeling</div>
  <div class="description">
    A complete PyTorch implementation of SASRec (Self-Attentive Sequential Recommendation),
    using multi-head self-attention to capture long-term dependencies in user interaction sequences,
    with positional embeddings and causal masking for autoregressive prediction.
  </div>
  <div class="metrics">
    📊 Metrics: Recall@10 = 80% | NDCG@10 = 59% (MovieLens 1M)
  </div>
  <div class="links">
    🔗 <a href="https://github.com/wujjjc/Sasrec">GitHub Repository</a>
  </div>
</div>

### 📌 GemiRec – Interest Quantization and Generation for Multi-Interest Recommendation

<div class="project">
  <div class="tech-stack">PyTorch | GPT | Vector Quantization (RQ-VAE) | ANN Retrieval</div>
  <div class="description">
    A generative multi-interest retrieval framework that enforces structural interest separation via quantization
    and explicitly models interest evolution via a generative model.<br>
    • <strong>IDMM</strong>: Residual quantization to map items to a discrete interest dictionary.<br>
    • <strong>MIPDM</strong>: 6-layer GPT to predict next interest distribution with Top‑K caching.<br>
    • <strong>MIRM</strong>: Multi-interest retrieval by fusing user and interest embeddings.
  </div>
  <div class="metrics">
    📊 Metrics: Amazon Books Recall@50 ↑12.6% | Industry Recall@200 ↑40.0% | Online CTR ↑0.38%
  </div>
  <div class="links">
    🔗 <a href="https://github.com/wujjjc/GemiRec">GitHub Repository</a>
  </div>
</div>

---

### 🔧 Other Projects

- **Tianchi Project**：[alitianchi](https://github.com/wujjjc/alitianchi)

---

### 📖 Study Notes

- [RQ-VAE Notes](https://www.cnblogs.com/GlenTt/p/19094976) (not written by me, for reference only)

---

## Contact

- GitHub: [@wujjjc](https://github.com/wujjjc)

</div>

<script>
  function setLanguage(lang) {
    var zh = document.getElementById('zh-content');
    var en = document.getElementById('en-content');
    if (lang === 'zh') {
      zh.style.display = 'block';
      en.style.display = 'none';
    } else {
      zh.style.display = 'none';
      en.style.display = 'block';
    }
    localStorage.setItem('lang', lang);
  }
  document.getElementById('btn-zh').addEventListener('click', function() { setLanguage('zh'); });
  document.getElementById('btn-en').addEventListener('click', function() { setLanguage('en'); });
  var savedLang = localStorage.getItem('lang');
  if (savedLang === 'en') setLanguage('en');
  else setLanguage('zh');
</script>
