---
layout: default
---

<div style="text-align: right; margin-bottom: 20px;">
  <button id="btn-zh">中文</button> | <button id="btn-en">English</button>
</div>

<div id="zh-content" style="display: block;">
  # 欢迎来到我的主页

  这是一个使用 **Cayman** 主题的个人网站。

  - 我的 GitHub: [@wujjjc](https://github.com/wujjjc)
  - 我的项目: [tianchi Project](https://github.com/wujjjc/alitianchi)
  - 我的项目: [Sasrec](https://github.com/wujjjc/Sasrec)
  - 我的项目: [GemiRec](https://github.com/wujjjc/GemiRec)
  - 学习日志(非本人写)：[rq-vae](https://www.cnblogs.com/GlenTt/p/19094976)
</div>

<div id="en-content" style="display: none;">
  # Welcome to My Homepage

  A personal website using the **Cayman** theme.

  - My GitHub: [@wujjjc](https://github.com/wujjjc)
  - My project: [tianchi Project](https://github.com/wujjjc/alitianchi)
  - My project: [Sasrec](https://github.com/wujjjc/Sasrec)
  - My project: [GemiRec](https://github.com/wujjjc/GemiRec)
  - Study log (not written by me): [rq-vae](https://www.cnblogs.com/GlenTt/p/19094976)
</div>

<script>
  function setLanguage(lang) {
    const zhDiv = document.getElementById('zh-content');
    const enDiv = document.getElementById('en-content');
    if (lang === 'zh') {
      zhDiv.style.display = 'block';
      enDiv.style.display = 'none';
    } else {
      zhDiv.style.display = 'none';
      enDiv.style.display = 'block';
    }
    // 可选：记住用户的选择（localStorage）
    localStorage.setItem('lang', lang);
  }

  document.getElementById('btn-zh').addEventListener('click', () => setLanguage('zh'));
  document.getElementById('btn-en').addEventListener('click', () => setLanguage('en'));

  // 页面加载时检查之前的选择
  const savedLang = localStorage.getItem('lang');
  if (savedLang === 'en') setLanguage('en');
  else setLanguage('zh');
</script>
