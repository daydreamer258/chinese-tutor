# Slide 制作技能 — 全流程 HTML 幻灯片生成

> 版本：v1.0
> 最后更新：2026-06-19
> 用途：从零开始完成 HTML 格式 slide 的制作全流程——信息收集 → 写脚本 → 编排设计 → 生成 HTML

---

## 触发条件

当用户要求以下任务时激活本技能：
- "做个 slides / PPT / 演示文稿"
- "把……做成幻灯片"
- "帮我做 presentation"
- "生成 HTML 格式的 slide"

---

## 全流程概览

```
Phase 1: 信息收集 → Phase 2: 写脚本大纲 → Phase 3: 编排设计 → Phase 4: 生成 HTML → Phase 5: 迭代优化
```

---

## Phase 1: 信息收集

### 目标
把用户提供的一切素材收集、整理成结构化的原始内容。

### 输入来源
- 用户直接描述的主题/内容
- 已有的文本、文档、笔记
- 网页内容（通过搜索获取）
- 数据和表格

### 操作
1. **确认主题和受众**：
   - "这个 slide 面向谁？（学生/同事/客户/大众）"
   - "时长大概多久？（5分钟/15分钟/30分钟）"
   - "核心想要传达什么信息？"

2. **搜集补充信息**：
   - 如果用户给的信息不够，主动搜索相关主题
   - 搜索关键词示例："[主题] 核心概念 关键数据"、"[主题] 最新发展 案例"

3. **整理成结构化原始稿**：
   - 用 Markdown 格式整理
   - 分板块：背景、核心观点、论据/数据、案例、总结
   - 标注信息缺口（告诉用户还缺什么）

---

## Phase 2: 写脚本大纲

### 目标
把原始内容转化为 slide-by-slide 的脚本。

### 设计原则
- **10-20-30 法则**：10 页以内（简洁）、20 分钟以内、字号不小于 30pt（对等）
- 高考语文类：15-20 页（适合完整教学）
- 普通场景：8-12 页

### 脚本格式（JSON）

每张 slide 包含以下字段：

```json
{
  "slides": [
    {
      "id": "slide-01",
      "title": "页标题",
      "role": "opener|context|point|example|data|summary|cta",
      "bullets": ["要点1（≤12字）", "要点2"],
      "visual": "图像/图表描述（可选）",
      "notes": "演讲者备注（可选）"
    }
  ]
}
```

### role 类型

| role | 用途 | 示例 |
|------|------|------|
| `opener` | 开场/标题页 | 标题+副标题+演讲者 |
| `context` | 背景介绍 | 为什么讲这个话题 |
| `point` | 核心观点 | 分论点阐述 |
| `example` | 案例/示例 | 具体例子说明 |
| `data` | 数据展示 | 图表、统计 |
| `summary` | 总结回顾 | 要点总结 |
| `cta` | 行动号召/结尾 | 下一步或结束语 |

### 大纲撰写步骤

1. **从原始稿中提炼核心结构**：开篇→主体(2-4个板块)→结尾
2. **每个核心观点分配 1-2 页**：不要一页塞太多
3. **给每页写 3-5 条 bullet**：每条不超过 12 个字（参考 TED 风格）
4. **产出 JSON 脚本**：提交给用户确认后再进入制作

---

## Phase 3: 编排设计

### 视觉设计系统

### 3.1 画面比例
- 默认 **16:9**（1280×720 或 1920×1080）

### 3.2 配色方案

提供 3 套预设主题：

**主题 A — 学术经典（适合教学、讲座）**
```json
{
  "bg": "#FFF8F0",
  "fg": "#2D3748",
  "accent": "#2B6CB0",
  "highlight": "#E53E3E",
  "muted": "#A0AEC0",
  "card": "#FFFFFF",
  "shadow": "rgba(0,0,0,0.08)"
}
```

**主题 B — 深色专业（适合技术、科技类）**
```json
{
  "bg": "#0F172A",
  "fg": "#E2E8F0",
  "accent": "#38BDF8",
  "highlight": "#F59E0B",
  "muted": "#64748B",
  "card": "#1E293B",
  "shadow": "rgba(0,0,0,0.3)"
}
```

**主题 C — 清新自然（适合文化、人文类）**
```json
{
  "bg": "#F7FAFC",
  "fg": "#1A202C",
  "accent": "#38A169",
  "highlight": "#DD6B20",
  "muted": "#A0AEC0",
  "card": "#FFFFFF",
  "shadow": "rgba(0,0,0,0.06)"
}
```

### 3.3 排版规格

| 元素 | 规范 |
|------|------|
| 标题 | h1, 字号 2.5-3rem, 居左或居中 |
| 副标题 | h2, 字号 1.5-2rem, 颜色 muted |
| 正文 bullet | 1.125rem (18px), 行高 1.8 |
| 卡片内文字 | 0.875-1rem |
| code | JetBrains Mono / Consolas, 0.9rem |
| 页面内边距 | 64-80px |
| 最大内容宽度 | 960px (居中) |

### 3.4 布局组件

HTML slide 使用的标准 class：

| 组件 | HTML | 用途 |
|------|------|------|
| 标准 slide | `<section class="slide">` | 基础页面 |
| 标题页 | `<section class="slide title-slide">` | 封面 |
| 两栏 | `<div class="cols">` + `<div class="col">` | 左右对比 |
| 三栏 | `<div class="cols three">` | 三点并列 |
| 卡片 | `<div class="card">` | 强调信息块 |
| 引用 | `<blockquote>` | 名言/引文 |
| 图表容器 | `<div class="chart">` | 数据图表占位 |
| 大数字 | `<div class="kpi">` | 关键指标展示 |
| 步骤条 | `<div class="steps">` + `<div class="step">` | 流程展示 |
| 图片框 | `<figure>` + `<figcaption>` | 配图说明 |

---

## Phase 4: 生成 HTML

### 技术选型：单文件 HTML + 内嵌 CSS/JS

**为什么用纯 HTML 单文件**：
- ✅ 零依赖，不需要 npm install
- ✅ 一个文件即可分享，双击打开浏览器就能看
- ✅ 完全自包含，离线可用
- ✅ 可以放在任何静态托管上

### HTML 模板结构

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>幻灯片标题</title>
  <style>
    /* === CSS 变量 & 主题 === */
    :root {
      --bg: #FFF8F0;
      --fg: #2D3748;
      --accent: #2B6CB0;
      --highlight: #E53E3E;
      --muted: #A0AEC0;
      --card: #FFFFFF;
      --shadow: rgba(0,0,0,0.08);
      --font-heading: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
      --font-body: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
    }

    /* === 基础 ===  */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: var(--font-body);
      background: var(--bg);
      color: var(--fg);
      overflow: hidden;
    }

    /* === 幻灯片容器 === */
    .reveal {
      width: 100vw;
      height: 100vh;
      position: relative;
    }

    .slide {
      width: 100vw;
      height: 100vh;
      display: none;
      flex-direction: column;
      justify-content: center;
      padding: 80px;
      position: absolute;
      top: 0; left: 0;
      opacity: 0;
      transition: opacity 0.4s ease;
    }

    .slide.active {
      display: flex;
      opacity: 1;
    }

    /* === 排版 === */
    .slide h1 {
      font-size: 2.8rem;
      font-weight: 700;
      color: var(--accent);
      margin-bottom: 24px;
      font-family: var(--font-heading);
    }

    .slide h2 {
      font-size: 1.8rem;
      font-weight: 500;
      color: var(--muted);
      margin-bottom: 16px;
    }

    .slide ul {
      list-style: none;
      margin: 20px 0;
    }

    .slide li {
      font-size: 1.2rem;
      line-height: 1.8;
      padding: 6px 0;
      position: relative;
      padding-left: 24px;
    }

    .slide li::before {
      content: "▸";
      position: absolute;
      left: 0;
      color: var(--accent);
      font-size: 1rem;
    }

    /* === 标题页 === */
    .title-slide {
      text-align: center;
      background: linear-gradient(135deg, var(--bg) 0%, var(--card) 100%);
    }

    .title-slide h1 {
      font-size: 3.5rem;
      margin-bottom: 16px;
    }

    .title-slide h2 {
      font-size: 1.4rem;
      font-weight: 400;
    }

    .title-slide .author {
      margin-top: 48px;
      font-size: 1rem;
      color: var(--muted);
    }

    /* === 布局 === */
    .cols {
      display: flex;
      gap: 40px;
      margin-top: 24px;
    }

    .col {
      flex: 1;
    }

    .cols.three { /* 三栏 */ }

    /* === 卡片 === */
    .card {
      background: var(--card);
      border-radius: 12px;
      padding: 28px;
      box-shadow: 0 2px 12px var(--shadow);
      margin: 8px 0;
    }

    .card h3 {
      color: var(--accent);
      margin-bottom: 12px;
      font-size: 1.2rem;
    }

    /* === 引用 === */
    blockquote {
      border-left: 4px solid var(--accent);
      padding: 16px 24px;
      font-size: 1.3rem;
      font-style: italic;
      color: var(--muted);
      margin: 24px 0;
      background: var(--card);
      border-radius: 0 8px 8px 0;
    }

    /* === KPI 大数字 === */
    .kpi {
      text-align: center;
      margin: 32px 0;
    }

    .kpi .number {
      font-size: 5rem;
      font-weight: 800;
      color: var(--accent);
      line-height: 1;
    }

    .kpi .label {
      font-size: 1.1rem;
      color: var(--muted);
      margin-top: 8px;
    }

    /* === 步骤条 === */
    .steps {
      display: flex;
      justify-content: space-between;
      margin: 40px 0;
    }

    .step {
      flex: 1;
      text-align: center;
      position: relative;
      padding: 0 16px;
    }

    .step::after {
      content: "";
      position: absolute;
      top: 24px;
      right: -50%;
      width: 100%;
      height: 3px;
      background: var(--muted);
      opacity: 0.3;
      transform: translateX(-50%);
    }

    .step:last-child::after { display: none; }

    .step .step-num {
      width: 48px;
      height: 48px;
      border-radius: 50%;
      background: var(--accent);
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 12px;
      font-weight: 700;
      font-size: 1.2rem;
    }

    .step .step-label {
      font-size: 0.95rem;
      color: var(--fg);
    }

    /* === 代码块 === */
    pre {
      background: #1E293B;
      color: #E2E8F0;
      padding: 24px;
      border-radius: 8px;
      font-size: 0.9rem;
      overflow-x: auto;
      margin: 16px 0;
    }

    code {
      font-family: 'JetBrains Mono', Consolas, monospace;
    }

    /* === 表格 === */
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 24px 0;
      background: var(--card);
      border-radius: 8px;
      overflow: hidden;
    }

    th {
      background: var(--accent);
      color: white;
      padding: 12px 16px;
      text-align: left;
      font-weight: 600;
    }

    td {
      padding: 10px 16px;
      border-bottom: 1px solid rgba(0,0,0,0.06);
    }

    /* === 图片 === */
    figure {
      margin: 24px 0;
      text-align: center;
    }

    figure img {
      max-width: 100%;
      max-height: 50vh;
      border-radius: 8px;
    }

    figcaption {
      color: var(--muted);
      font-size: 0.85rem;
      margin-top: 8px;
    }

    /* === 导航 === */
    .nav {
      position: fixed;
      bottom: 24px;
      right: 32px;
      display: flex;
      gap: 12px;
      z-index: 100;
    }

    .nav button {
      background: var(--card);
      border: 1px solid var(--muted);
      color: var(--fg);
      padding: 8px 16px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 0.9rem;
      transition: all 0.2s;
    }

    .nav button:hover {
      background: var(--accent);
      color: white;
      border-color: var(--accent);
    }

    .page-num {
      position: fixed;
      bottom: 28px;
      left: 32px;
      color: var(--muted);
      font-size: 0.85rem;
      z-index: 100;
    }

    /* === 动画 === */
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .slide.active h1,
    .slide.active li,
    .slide.active .card {
      animation: fadeInUp 0.5s ease forwards;
    }

    .slide.active li:nth-child(2) { animation-delay: 0.1s; }
    .slide.active li:nth-child(3) { animation-delay: 0.2s; }
    .slide.active li:nth-child(4) { animation-delay: 0.3s; }
    .slide.active li:nth-child(5) { animation-delay: 0.4s; }

    /* === 打印/响应式 === */
    @media print {
      body { overflow: visible; }
      .slide {
        position: relative;
        display: flex !important;
        opacity: 1 !important;
        page-break-after: always;
        height: 100vh;
      }
      .nav, .page-num { display: none; }
    }

    @media (max-width: 768px) {
      .slide { padding: 40px; }
      .slide h1 { font-size: 1.8rem; }
      .cols { flex-direction: column; }
    }
  </style>
</head>
<body>

  <div class="reveal">
    <!-- 幻灯片内容在这里 -->
  </div>

  <div class="nav">
    <button onclick="prevSlide()">◀ 上一页</button>
    <button onclick="nextSlide()">下一页 ▶</button>
  </div>

  <div class="page-num">
    <span id="current-page">1</span> / <span id="total-pages">1</span>
  </div>

  <script>
    let currentSlide = 0;
    const slides = document.querySelectorAll('.slide');
    const totalPagesEl = document.getElementById('total-pages');
    totalPagesEl.textContent = slides.length;

    function showSlide(index) {
      slides.forEach((s, i) => {
        s.classList.toggle('active', i === index);
      });
      document.getElementById('current-page').textContent = index + 1;
    }

    function nextSlide() {
      currentSlide = Math.min(currentSlide + 1, slides.length - 1);
      showSlide(currentSlide);
    }

    function prevSlide() {
      currentSlide = Math.max(currentSlide - 1, 0);
      showSlide(currentSlide);
    }

    document.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowRight' || e.key === 'ArrowDown' || e.key === ' ') {
        e.preventDefault(); nextSlide();
      } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
        e.preventDefault(); prevSlide();
      } else if (e.key === 'Home') {
        e.preventDefault(); currentSlide = 0; showSlide(0);
      } else if (e.key === 'End') {
        e.preventDefault(); currentSlide = slides.length - 1; showSlide(currentSlide);
      }
    });

    showSlide(0);
  </script>
</body>
</html>
```

### 每张 slide 的 HTML 结构

```html
<!-- 标题页 -->
<section class="slide title-slide active">
  <h1>演示文稿标题</h1>
  <h2>副标题 / 一句话描述</h2>
  <p class="author">演讲者 · 日期</p>
</section>

<!-- 标准内容页 -->
<section class="slide">
  <h1>页面标题</h1>
  <div class="cols">
    <div class="col">
      <ul>
        <li>要点一：用简洁的语言概括</li>
        <li>要点二：每条不超过 12 字</li>
        <li>要点三：用 bullet 分条</li>
      </ul>
    </div>
    <div class="col">
      <div class="card">
        <h3>补充说明</h3>
        <p>这里放关键数据、引言或备注</p>
      </div>
    </div>
  </div>
</section>

<!-- 引用页 -->
<section class="slide">
  <blockquote>「教育不是注满一桶水，而是点燃一把火。」</blockquote>
  <p style="text-align:right; color: var(--muted);">— 叶芝</p>
</section>

<!-- 总结页 -->
<section class="slide">
  <h1>总结</h1>
  <div class="cols three">
    <div class="card">
      <h3>要点一</h3>
      <p>一句话总结</p>
    </div>
    <div class="card">
      <h3>要点二</h3>
      <p>一句话总结</p>
    </div>
    <div class="card">
      <h3>要点三</h3>
      <p>一句话总结</p>
    </div>
  </div>
</section>

<!-- 结束页 -->
<section class="slide title-slide">
  <h1>谢谢</h1>
  <h2>Q & A</h2>
  <p class="author">联系方式 / 二维码 / 下一步行动</p>
</section>
```

### 生成规范

1. **单文件输出**：CSS + JS + HTML 全部内嵌在一个文件里
2. **文件名**：`slides_[主题简称].html`
3. **编码**：UTF-8，带 `<meta charset="UTF-8">`
4. **字体**：优先使用系统自带中文字体（PingFang SC, Microsoft YaHei），不依赖外部 CDN
5. **图片**：如有图片，用 base64 内嵌或 placeholder SVG（避免外部链接失效）
6. **键盘导航**：← → 翻页，Home/End 跳首尾，Space 下一页

---

## Phase 5: 迭代优化

### 支持的迭代操作

1. **内容修改**
   - "把第 3 页的第 2 条 bullet 改成……"
   - "在第 5 页后面加一页关于……的 slide"

2. **结构调整**
   - "拆分这一页为两页"
   - "把第 4 和第 5 页顺序调换"

3. **视觉微调**
   - "整体调暗 / 调亮"
   - "把主题色换成红色系"
   - "标题字号加大 20%"

4. **功能增强**
   - "加入一个目录页"
   - "加入演讲者备注"
   - "导出为 PDF 的建议"

### 迭代实现方式

- 直接在已有的 HTML 文件中修改对应部分
- 如果是新增 slide，插入新的 `<section class="slide">`
- 如果是改样式，修改 `<style>` 中的 CSS 变量

---

## 质量检查清单

生成 HTML 后必须检查：

- [ ] 文件是一个完整的、可直接打开的 .html 文件
- [ ] 在浏览器中打开可正常显示
- [ ] ← → 键盘翻页正常
- [ ] 页码显示正确
- [ ] 每页内容不溢出屏幕（不出现滚动条）
- [ ] bullet 用 `<ul><li>` 而非纯文本
- [ ] 中文排版正常，无乱码
- [ ] 配色协调，文字可读
- [ ] 移动端/小屏有基本 layout 适应

---

## 全流程速查

| 阶段 | 输入 | 输出 | 给用户确认？ |
|------|------|------|------------|
| 收集 | 用户描述/搜索 | 结构化原始稿 | ✅ 确认再继续 |
| 脚本 | 原始稿 | JSON 脚本大纲 | ✅ 确认再继续 |
| 编排 | 脚本大纲 | 配色方案+布局选择 | 可选 |
| 生成 | 脚本+设计 | HTML 文件 | ❌ 直接生成 |
| 迭代 | 用户反馈 | 修改后的 HTML | ❌ 直接修改 |
