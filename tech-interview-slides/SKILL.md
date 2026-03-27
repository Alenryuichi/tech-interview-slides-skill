---
name: tech-deep-dive-slides
description: 创建高信息密度的技术深度解析演示文稿。Neon Cyber 深色科技风格，支持深度解析弹窗、架构图、代码块、知识图谱式导航。适用于技术学习、架构分享、项目展示、开源项目解析。
triggers:
  - 技术 PPT
  - 技术演示
  - presentation
  - slides
  - 幻灯片
  - 架构分享
  - 项目展示
  - tech presentation
  - 技术深度解析
  - 开源项目解析
---

# Tech Deep-Dive Slides Skill

> **核心理念**: 单 HTML 文件，零依赖，将任意技术项目转化为可交互的高信息密度演示文稿。每页承载核心概要，深度解析弹窗展开完整技术细节。

## 何时使用

- 用户说："帮我做一个技术深度解析的 PPT"
- 用户说："创建项目展示的幻灯片"
- 用户说："做一个架构分享的演示文稿"
- 用户说："帮我分析这个开源项目，生成 PPT"

## 核心原则

| 原则 | 说明 |
|------|------|
| **高信息密度** | 每页承载大量技术要点，通过卡片、网格、标签组织 |
| **深度解析弹窗** | 主幻灯片展示概览，点击"深度解析"展开详情（代码、架构、设计模式） |
| **零依赖** | 单 HTML 文件，内联 CSS/JS，仅外链 Fontshare 字体 |
| **视口适配** | 每页 100dvh，clamp() 响应式，打印友好 |
| **技术学习导向** | 每个技术点关注"是什么 → 为什么 → 怎么实现 → 设计模式" |

---

## HTML 文档结构

完整 HTML 文档由三部分组成：Fixed Chrome（固定 UI）、Slides（幻灯片序列）、Modals（深度解析弹窗）。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>项目名 — 技术架构深度解析</title>
    <link rel="stylesheet" href="https://api.fontshare.com/v2/css?f[]=clash-display@400,500,600,700&f[]=satoshi@400,500,700&display=swap">
    <style>/* 所有 CSS 内联 */</style>
</head>
<body>
<!-- Fixed Chrome -->
<div class="progress-bar" id="progressBar"></div>
<div class="nav-container" id="navDots"></div>
<div class="slide-counter" id="slideNumber"></div>
<div class="help-overlay" id="helpOverlay"><!-- 快捷键帮助面板 --></div>

<!-- Slides -->
<section class="slide gradient-bg grid-bg">...</section>
<section class="slide gradient-bg grid-bg">...</section>
...

<!-- Modals -->
<div class="modal-overlay" id="modal-xxx">...</div>
...

<script>/* 所有 JS 内联 */</script>
</body>
</html>
```

### Fixed Chrome 详细结构

#### 进度条

```html
<div class="progress-bar" id="progressBar"></div>
```

#### 导航点（由 JS 注入）

```html
<div class="nav-container" id="navDots"></div>
```

#### 页码计数器

```html
<div class="slide-counter" id="slideNumber"></div>
```

#### 快捷键帮助面板

```html
<div class="help-overlay" id="helpOverlay">
    <div class="help-content">
        <h3>Keyboard Shortcuts</h3>
        <div class="help-row"><span>Next slide</span><span><span class="help-key">→</span> <span class="help-key">↓</span> <span class="help-key">Space</span></span></div>
        <div class="help-row"><span>Previous slide</span><span><span class="help-key">←</span> <span class="help-key">↑</span></span></div>
        <div class="help-row"><span>First / Last</span><span><span class="help-key">Home</span> <span class="help-key">End</span></span></div>
        <div class="help-row"><span>Open deep dive</span><span><span class="help-key">Enter</span> <span class="help-key">D</span></span></div>
        <div class="help-row"><span>Close modal</span><span><span class="help-key">Esc</span></span></div>
        <div class="help-row"><span>This help</span><span><span class="help-key">?</span></span></div>
        <div style="margin-top:1rem;font-size:0.8rem;color:var(--text-secondary);">Touch: swipe up/down to navigate</div>
    </div>
</div>
```

---

## 风格规范：Neon Cyber

### CSS 变量（必须完整复制到 :root）

```css
:root {
    --bg-primary: #0a0a0f;
    --bg-secondary: #12121a;
    --bg-tertiary: #1a1a24;
    --text-primary: #ffffff;
    --text-secondary: #a0a0b0;
    --accent: #00ff88;
    --accent-secondary: #00ccff;
    --accent-glow: rgba(0, 255, 136, 0.3);
    --orange: #fd6f32;
    --orange-glow: rgba(253, 111, 50, 0.3);
    --font-display: 'Clash Display', sans-serif;
    --font-body: 'Satoshi', sans-serif;
    --title-size: clamp(2rem, 5vw, 4rem);
    --h2-size: clamp(1.5rem, 3.5vw, 2.5rem);
    --h3-size: clamp(1.1rem, 2vw, 1.5rem);
    --body-size: clamp(0.8rem, 1.3vw, 1.1rem);
    --small-size: clamp(0.7rem, 1vw, 0.9rem);
    --slide-padding: clamp(1.5rem, 4vw, 3rem);
}
```

### 全局基础样式

```css
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; scroll-snap-type: y mandatory; overflow-x: hidden; }
body { background: var(--bg-primary); color: var(--text-primary); font-family: var(--font-body); line-height: 1.6; }
h1 { font-family: var(--font-display); font-size: var(--title-size); font-weight: 700; line-height: 1.15; }
h2 { font-family: var(--font-display); font-size: var(--h2-size); font-weight: 600; line-height: 1.2; margin-bottom: 1rem; }
h3 { font-family: var(--font-display); font-size: var(--h3-size); font-weight: 600; line-height: 1.3; }
p { font-size: var(--body-size); color: var(--text-secondary); }
```

### 幻灯片基础 + 进入动画

```css
.slide {
    min-height: 100dvh;
    scroll-snap-align: start;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: var(--slide-padding);
    opacity: 0;
    transform: translateY(10px);
    transition: opacity 0.5s ease, transform 0.5s ease;
}
.slide.visible { opacity: 1; transform: translateY(0); }
.slide-content { max-width: 1100px; width: 100%; }
```

### 背景效果

```css
.gradient-bg {
    background:
        radial-gradient(ellipse 80% 50% at 50% -20%, rgba(0,255,136,0.15), transparent),
        radial-gradient(ellipse 60% 40% at 80% 50%, rgba(0,204,255,0.08), transparent),
        radial-gradient(ellipse 50% 30% at 20% 80%, rgba(253,111,50,0.05), transparent);
}
.grid-bg {
    background-image:
        linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
}
```

### Section Label + 脉冲动画

```css
.section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: var(--small-size);
    font-weight: 500;
    color: var(--accent);
    letter-spacing: 0.08em;
    display: flex;
    align-items: center;
    gap: 0.6rem;
    margin-bottom: 0.8rem;
}
.section-label::before {
    content: '';
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--accent);
    box-shadow: 0 0 8px var(--accent-glow);
    animation: pulse 2s infinite;
}
@keyframes pulse {
    0%, 100% { box-shadow: 0 0 8px var(--accent-glow); }
    50% { box-shadow: 0 0 16px var(--accent-glow); }
}
```

### Fixed Chrome CSS

```css
.progress-bar {
    position: fixed; top: 0; left: 0; height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent-secondary));
    z-index: 999; transition: width 0.3s;
}
.nav-container {
    position: fixed; right: 1.5rem; top: 50%; transform: translateY(-50%);
    display: flex; flex-direction: column; gap: 6px; z-index: 999;
}
.nav-dot {
    width: 8px; height: 8px; border-radius: 50%;
    background: rgba(255,255,255,0.2); border: none;
    cursor: pointer; transition: all 0.3s; padding: 0;
}
.nav-dot.active {
    background: var(--accent);
    box-shadow: 0 0 8px var(--accent-glow);
    transform: scale(1.4);
}
.slide-counter {
    position: fixed; bottom: 1.5rem; left: 1.5rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.8rem; color: var(--text-secondary); z-index: 999;
}
.help-overlay {
    position: fixed; inset: 0; background: rgba(0,0,0,0.9);
    display: flex; align-items: center; justify-content: center;
    z-index: 2000; opacity: 0; visibility: hidden;
    transition: opacity 0.3s, visibility 0.3s;
}
.help-overlay.active { opacity: 1; visibility: visible; }
.help-content {
    background: var(--bg-secondary);
    border: 1px solid rgba(255,255,255,0.15);
    border-radius: 16px; padding: 2rem;
    max-width: 500px; width: 90%;
}
.help-content h3 { font-family: var(--font-display); color: var(--accent); margin-bottom: 1rem; }
.help-row {
    display: flex; justify-content: space-between;
    padding: 0.4rem 0; border-bottom: 1px solid rgba(255,255,255,0.06);
    font-size: 0.9rem;
}
.help-key {
    font-family: 'JetBrains Mono', monospace;
    background: var(--bg-tertiary);
    padding: 0.15em 0.5em; border-radius: 4px;
    border: 1px solid rgba(255,255,255,0.15);
    font-size: 0.85em;
}
```

### 响应式 + 打印

```css
@media (max-width: 768px) {
    .nav-container { right: 0.5rem; }
    .nav-dot { width: 6px; height: 6px; }
}

@media print {
    .slide { min-height: auto; page-break-after: always; opacity: 1 !important; transform: none !important; padding: 1rem; }
    .nav-container, .slide-counter, .progress-bar, .detail-btn, .help-overlay { display: none !important; }
    .modal-overlay { position: relative; opacity: 1 !important; visibility: visible !important; background: white; page-break-before: always; }
    .modal-content { max-height: none; max-width: 100%; border: 1px solid #ccc; }
    body { background: white; color: black; }
}
```

---

## 核心组件库

### 1. 基础幻灯片结构

每个幻灯片都使用此结构：

```html
<section class="slide gradient-bg grid-bg">
    <div class="slide-content">
        <span class="section-label">SECTION_NAME</span>
        <h2>幻灯片标题</h2>
        <!-- 内容组件 -->
    </div>
    <button class="detail-btn" onclick="openModal('modal-id')">深度解析</button>
</section>
```

### 2. Problem / Solution / Why Box

```html
<div class="problem-box">
    <div class="problem-label">问题</div>
    <p>问题描述</p>
</div>

<div class="solution-box">
    <div class="solution-label">方案</div>
    <p>方案描述</p>
</div>

<div class="why-box">
    <div class="why-label">设计哲学</div>
    <p><strong>核心原则</strong> — 解释</p>
</div>
```

```css
.problem-box { background: rgba(248,113,113,0.08); border: 1px solid rgba(248,113,113,0.2); border-left: 3px solid #f87171; border-radius: 8px; padding: clamp(0.6rem,1.2vw,1rem) clamp(0.8rem,1.5vw,1.2rem); margin-bottom: 0.6rem; }
.problem-label { color: #f87171; font-weight: 600; font-size: 0.85em; margin-bottom: 0.2rem; }
.solution-box { background: rgba(52,211,153,0.08); border: 1px solid rgba(52,211,153,0.2); border-left: 3px solid #34d399; border-radius: 8px; padding: clamp(0.6rem,1.2vw,1rem) clamp(0.8rem,1.5vw,1.2rem); margin-bottom: 0.6rem; }
.solution-label { color: #34d399; font-weight: 600; font-size: 0.85em; margin-bottom: 0.2rem; }
.why-box { background: rgba(0,255,136,0.06); border: 1px solid rgba(0,255,136,0.2); border-left: 3px solid var(--accent); border-radius: 8px; padding: clamp(0.6rem,1.2vw,1rem) clamp(0.8rem,1.5vw,1.2rem); margin-bottom: 0.6rem; }
.why-label { color: var(--accent); font-weight: 600; font-size: 0.85em; margin-bottom: 0.2rem; }
```

### 3. Flow Node (流程图)

```html
<div class="flow">
    <div class="flow-node">Input</div>
    <span class="flow-arrow">→</span>
    <div class="flow-node active">Processing</div>
    <span class="flow-arrow">→</span>
    <div class="flow-node success">Output</div>
</div>
```

```css
.flow { display: flex; align-items: center; gap: 0.5rem; flex-wrap: wrap; margin: 0.8rem 0; }
.flow-node { font-family: 'JetBrains Mono', monospace; font-size: clamp(0.6rem,0.9vw,0.8rem); padding: 0.4em 0.8em; border-radius: 6px; background: var(--bg-tertiary); border: 1px solid rgba(255,255,255,0.1); color: var(--text-secondary); transition: border-color 0.3s; }
.flow-node.active { border-color: rgba(0,255,136,0.3); color: var(--accent); background: rgba(0,255,136,0.1); }
.flow-node.success { border-color: rgba(52,211,153,0.3); color: #34d399; background: rgba(52,211,153,0.1); }
.flow-node.warn { border-color: rgba(251,191,36,0.3); color: #fbbf24; background: rgba(251,191,36,0.1); }
.flow-node.blue { border-color: rgba(99,102,241,0.3); color: #818cf8; background: rgba(99,102,241,0.1); }
.flow-arrow { color: var(--accent); font-size: 1.2em; }
```

### 4. Architecture Diagram (架构层级图)

```html
<div class="arch-diagram">
    <div class="arch-layer">
        <span class="arch-layer-name">Entry Layer</span>
        <div class="arch-layer-content">
            <span class="arch-item">Component A</span>
            <span class="arch-item">Component B</span>
        </div>
    </div>
    <div class="arch-layer orange">
        <span class="arch-layer-name">Core Engine</span>
        <div class="arch-layer-content">
            <span class="arch-item orange">Module X</span>
        </div>
    </div>
    <div class="arch-layer blue">
        <span class="arch-layer-name">Data Layer</span>
        <div class="arch-layer-content">
            <span class="arch-item blue">Store</span>
        </div>
    </div>
    <div class="arch-layer purple">
        <span class="arch-layer-name">Extensions</span>
        <div class="arch-layer-content">
            <span class="arch-item purple">Plugin</span>
        </div>
    </div>
</div>
```

```css
.arch-diagram { display: flex; flex-direction: column; gap: 0.5rem; margin: 0.8rem 0; }
.arch-layer { background: var(--bg-secondary); border: 1px solid rgba(0,255,136,0.15); border-radius: 8px; padding: 0.5rem 0.8rem; display: flex; align-items: center; gap: 0.8rem; }
.arch-layer.orange { border-color: rgba(253,111,50,0.3); }
.arch-layer.blue { border-color: rgba(0,204,255,0.3); }
.arch-layer.purple { border-color: rgba(168,85,247,0.3); }
.arch-layer-name { font-family: 'JetBrains Mono', monospace; font-size: clamp(0.6rem,0.85vw,0.75rem); color: var(--accent); min-width: 100px; font-weight: 600; }
.arch-layer.orange .arch-layer-name { color: var(--orange); }
.arch-layer.blue .arch-layer-name { color: var(--accent-secondary); }
.arch-layer.purple .arch-layer-name { color: #a855f7; }
.arch-layer-content { display: flex; gap: 0.4rem; flex-wrap: wrap; }
.arch-item { font-family: 'JetBrains Mono', monospace; font-size: clamp(0.55rem,0.8vw,0.7rem); padding: 0.25em 0.6em; border-radius: 4px; background: rgba(0,255,136,0.08); color: var(--accent); border: 1px solid rgba(0,255,136,0.15); }
.arch-item.orange { background: rgba(253,111,50,0.08); color: var(--orange); border-color: rgba(253,111,50,0.15); }
.arch-item.blue { background: rgba(0,204,255,0.08); color: var(--accent-secondary); border-color: rgba(0,204,255,0.15); }
.arch-item.purple { background: rgba(168,85,247,0.08); color: #a855f7; border-color: rgba(168,85,247,0.15); }
```

### 5. Code Block (代码块)

幻灯片内的代码块使用 `.code-block`，模态框内使用 `.modal-code`。

```html
<div class="code-block">
    <pre><span class="comment"># 核心逻辑</span>
<span class="keyword">async def</span> <span class="function">train_step</span>(self, batch):
    loss = model(<span class="string">"input"</span>)
    <span class="keyword">return</span> loss</pre>
</div>
```

```css
.code-block { background: var(--bg-secondary); border: 1px solid rgba(0,255,136,0.2); border-radius: 8px; padding: clamp(0.75rem,1.5vw,1rem); font-family: 'JetBrains Mono','Fira Code',monospace; font-size: clamp(0.65rem,0.9vw,0.85rem); overflow-x: auto; line-height: 1.5; }
.code-block .keyword { color: #ff79c6; }
.code-block .string { color: #f1fa8c; }
.code-block .function { color: #50fa7b; }
.code-block .comment { color: #6272a4; }
.code-block .class { color: #8be9fd; }

.modal-code { background: rgba(0,0,0,0.4); border: 1px solid rgba(255,255,255,0.1); border-radius: 8px; padding: 1rem; font-family: 'JetBrains Mono', monospace; font-size: 0.75rem; line-height: 1.5; white-space: pre-wrap; word-break: break-word; overflow-x: auto; }
```

### 6. Inline Code

```css
code { background: rgba(0,255,136,0.1); color: var(--accent); padding: 0.2em 0.4em; border-radius: 3px; font-family: 'JetBrains Mono', monospace; font-size: 0.9em; }
```

### 7. Stat Card (统计卡片)

```html
<div class="stat-grid">
    <div class="stat-card">
        <div class="stat-number">17+</div>
        <div class="stat-label">模型支持</div>
    </div>
    <div class="stat-card">
        <div class="stat-number orange">5 min</div>
        <div class="stat-label">训练时间</div>
    </div>
    <div class="stat-card">
        <div class="stat-number blue">1.2B</div>
        <div class="stat-label">参数量</div>
    </div>
</div>
```

```css
.stat-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(120px, 1fr)); gap: clamp(0.5rem,1vw,1rem); }
.stat-card { background: var(--bg-secondary); border: 1px solid rgba(255,255,255,0.1); border-radius: 12px; padding: clamp(0.75rem,1.5vw,1.25rem); text-align: center; transition: border-color 0.3s; }
.stat-card:hover { border-color: rgba(0,255,136,0.3); }
.stat-number { font-family: 'Clash Display', sans-serif; font-size: clamp(1.5rem,3vw,2.5rem); font-weight: 700; color: var(--accent); line-height: 1.2; }
.stat-number.orange { color: var(--orange); }
.stat-number.blue { color: var(--accent-secondary); }
.stat-label { font-size: var(--small-size); color: var(--text-secondary); }
```

### 8. Modal Tag (技术标签)

```html
<span class="modal-tag">Design Pattern</span>
<span class="modal-tag">Strategy</span>
```

```css
.modal-tag { display: inline-block; background: rgba(99,102,241,0.2); color: var(--accent-secondary); padding: 0.2em 0.6em; border-radius: 4px; font-size: 0.75rem; margin-right: 0.3em; margin-bottom: 0.3em; }
```

### 9. Title Page Components

```css
.logo { font-family: var(--font-display); font-size: clamp(1.2rem,2vw,1.6rem); font-weight: 700; color: var(--accent); margin-bottom: 1rem; }
.logo span { color: var(--text-secondary); font-weight: 400; font-size: 0.7em; }
.subtitle { font-size: clamp(0.9rem,1.5vw,1.2rem); color: var(--text-secondary); margin-top: 0.8rem; }
.meta { margin-top: 1.5rem; font-family: 'JetBrains Mono', monospace; font-size: var(--small-size); color: var(--text-secondary); opacity: 0.7; }
```

### 10. Challenge Card (难点卡片)

六色变体，用于展示"难点 + 解决方案"配对：

```html
<div style="display:grid;grid-template-columns:repeat(2,1fr);gap:0.5rem;">
    <div style="background:rgba(239,68,68,0.05);border:1px solid rgba(239,68,68,0.3);border-radius:8px;padding:0.5rem;">
        <div style="display:flex;align-items:center;gap:0.3rem;margin-bottom:0.3rem;">
            <span style="background:#ef4444;color:white;padding:0.1rem 0.4rem;border-radius:4px;font-size:0.75em;font-weight:600;">难点 1</span>
            <strong style="color:#f87171;">问题标题</strong>
        </div>
        <p style="font-size:0.85em;color:var(--text-secondary);">问题描述</p>
        <div style="background:rgba(52,211,153,0.1);border-left:3px solid #34d399;padding:0.3rem 0.5rem;margin-top:0.3rem;">
            <strong style="color:#34d399;font-size:0.8em;">✅ 解决方案</strong>
        </div>
    </div>
</div>
```

颜色变体：

| # | 背景 | 边框/标签 |
|---|------|----------|
| 1 | `rgba(239,68,68,0.05)` | `#ef4444` 红 |
| 2 | `rgba(249,115,22,0.05)` | `#f97316` 橙 |
| 3 | `rgba(234,179,8,0.05)` | `#eab308` 黄 |
| 4 | `rgba(99,102,241,0.05)` | `#6366f1` 靛 |
| 5 | `rgba(236,72,153,0.05)` | `#ec4899` 粉 |
| 6 | `rgba(20,184,166,0.05)` | `#14b8a6` 青 |

### 11. Table (表格)

```html
<table style="width:100%;font-size:0.9em;border-collapse:collapse;">
    <tr style="border-bottom:1px solid rgba(255,255,255,0.2);background:rgba(255,255,255,0.05);">
        <th style="text-align:left;padding:0.5em;">维度</th>
        <th style="text-align:center;padding:0.5em;">选项 A</th>
        <th style="text-align:center;padding:0.5em;">选项 B</th>
    </tr>
    <tr style="border-bottom:1px solid rgba(255,255,255,0.1);">
        <td style="padding:0.5em;">特性</td>
        <td style="text-align:center;padding:0.5em;">值</td>
        <td style="text-align:center;padding:0.5em;color:var(--accent);">✅ 值</td>
    </tr>
</table>
```

---

## 深度解析弹窗 (Detail Modal)

每个技术幻灯片可配套一个深度解析弹窗。

### 触发按钮

```css
.detail-btn {
    position: absolute;
    bottom: calc(var(--slide-padding) + 0.5rem);
    right: calc(var(--slide-padding) + 0.5rem);
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent-secondary) 100%);
    color: var(--bg-primary); border: none;
    padding: 0.6em 1.2em; border-radius: 8px;
    font-weight: 600; cursor: pointer;
    box-shadow: 0 4px 20px var(--accent-glow);
    z-index: 100; transition: transform 0.2s, box-shadow 0.2s;
    font-family: var(--font-body); font-size: var(--small-size);
}
.detail-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 25px var(--accent-glow); }
.detail-btn::before { content: '\1F4D6'; margin-right: 0.4em; }
```

### 弹窗容器

```css
.modal-overlay {
    position: fixed; inset: 0;
    background: rgba(0,0,0,0.85);
    backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
    display: flex; align-items: center; justify-content: center;
    z-index: 1000; opacity: 0; visibility: hidden;
    transition: opacity 0.3s, visibility 0.3s;
}
.modal-overlay.active { opacity: 1; visibility: visible; }
.modal-content {
    background: var(--bg-secondary);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 16px;
    padding: clamp(1.5rem,3vw,2.5rem);
    max-width: 900px; width: 90%; max-height: 85vh;
    overflow-y: auto; position: relative;
    transform: translateY(20px) scale(0.98);
    transition: transform 0.3s;
}
.modal-overlay.active .modal-content { transform: translateY(0) scale(1); }
.modal-close {
    position: absolute; top: 1rem; right: 1rem;
    background: rgba(255,255,255,0.1); border: none;
    color: var(--text-secondary); width: 32px; height: 32px;
    border-radius: 50%; cursor: pointer; font-size: 1rem;
    display: flex; align-items: center; justify-content: center;
    transition: background 0.2s;
}
.modal-close:hover { background: rgba(255,255,255,0.2); }
.modal-title { font-family: var(--font-display); font-size: clamp(1.2rem,2.5vw,1.8rem); font-weight: 600; margin-bottom: 1.5rem; color: var(--text-primary); }
```

### 弹窗内部组件

```css
.modal-section { margin-bottom: 1.5rem; }
.modal-section h4 { color: var(--accent-secondary); font-size: 1rem; margin-bottom: 0.5rem; display: flex; align-items: center; gap: 0.5em; }
.modal-section ul { margin-left: 1.2rem; color: var(--text-secondary); font-size: 0.9rem; }
.modal-section li { margin-bottom: 0.3rem; }
.modal-section p { font-size: 0.9rem; }
.strategy-card { border: 1px solid rgba(255,255,255,0.15); border-radius: 8px; padding: 0.8rem; margin-bottom: 0.6rem; background: rgba(255,255,255,0.03); }
.strategy-card h5 { color: var(--accent); font-size: 0.95rem; margin-bottom: 0.4rem; }
.modal-highlight { background: rgba(0,255,136,0.1); border-left: 3px solid var(--accent); padding: 0.8rem 1rem; border-radius: 0 8px 8px 0; margin-top: 0.5rem; font-size: 0.9rem; }
```

### 弹窗 HTML 结构模板

```html
<div class="modal-overlay" id="modal-xxx">
    <div class="modal-content">
        <button class="modal-close" onclick="closeModal('modal-xxx')">✕</button>
        <h3 class="modal-title">模块名称 — 深度解析</h3>

        <div class="modal-section">
            <h4>核心概念</h4>
            <p>一句话定义 + 为什么需要这个模块</p>
            <ul>
                <li><strong>概念 A</strong> — 解释</li>
                <li><strong>概念 B</strong> — 解释</li>
            </ul>
        </div>

        <div class="modal-section">
            <h4>架构设计</h4>
            <div class="strategy-card">
                <h5>组件名称</h5>
                <ul><li>实现细节</li></ul>
            </div>
        </div>

        <div class="modal-section">
            <h4>实现细节</h4>
            <div class="modal-code">// 真实代码片段
function core() { ... }</div>
        </div>

        <div class="modal-section">
            <h4>相关设计模式</h4>
            <p>
                <span class="modal-tag">Pattern A</span>
                <span class="modal-tag">Pattern B</span>
                <span class="modal-tag">Pattern C</span>
            </p>
            <div class="modal-highlight">
                <strong>核心思路：</strong>用一句话总结设计哲学。
            </div>
        </div>
    </div>
</div>
```

---

## JavaScript 功能

完整的导航控制器，必须原样使用：

```javascript
(function() {
    const slides = document.querySelectorAll('.slide');
    const progressBar = document.getElementById('progressBar');
    const navDots = document.getElementById('navDots');
    const slideNumber = document.getElementById('slideNumber');
    const totalSlides = slides.length;
    let currentSlide = 0;

    slides.forEach((_, i) => {
        const d = document.createElement('button');
        d.className = 'nav-dot';
        d.setAttribute('aria-label', `Slide ${i+1}`);
        d.addEventListener('click', () => goToSlide(i));
        navDots.appendChild(d);
    });
    const dots = document.querySelectorAll('.nav-dot');

    function updateSlideState() {
        progressBar.style.width = `${((currentSlide+1)/totalSlides)*100}%`;
        slideNumber.textContent = `${currentSlide+1} / ${totalSlides}`;
        dots.forEach((d,i) => d.classList.toggle('active', i===currentSlide));
        slides.forEach((s,i) => s.classList.toggle('visible', i===currentSlide));
    }

    window.goToSlide = function goToSlide(i) {
        if (i>=0 && i<totalSlides) {
            currentSlide = i;
            slides[i].scrollIntoView({behavior:'smooth'});
            updateSlideState();
        }
    }

    document.addEventListener('keydown', e => {
        if (document.getElementById('helpOverlay').classList.contains('active')) {
            document.getElementById('helpOverlay').classList.remove('active');
            return;
        }
        if (document.querySelector('.modal-overlay.active')) return;
        switch(e.key) {
            case 'ArrowRight': case 'ArrowDown': case ' ': case 'PageDown':
                e.preventDefault(); goToSlide(currentSlide+1); break;
            case 'ArrowLeft': case 'ArrowUp': case 'PageUp':
                e.preventDefault(); goToSlide(currentSlide-1); break;
            case 'Home': e.preventDefault(); goToSlide(0); break;
            case 'End': e.preventDefault(); goToSlide(totalSlides-1); break;
            case 'Enter': case 'd': case 'D':
                e.preventDefault();
                var btn = slides[currentSlide].querySelector('.detail-btn');
                if (btn) btn.click();
                break;
            case '?':
                e.preventDefault();
                document.getElementById('helpOverlay').classList.toggle('active');
                break;
        }
    });

    let isScrolling = false;
    document.addEventListener('wheel', e => {
        if (document.querySelector('.modal-overlay.active')) return;
        if (isScrolling) return;
        isScrolling = true;
        if (e.deltaY > 0) goToSlide(currentSlide+1);
        else goToSlide(currentSlide-1);
        setTimeout(() => { isScrolling = false; }, 800);
    }, {passive: true});

    let touchStartY = 0;
    document.addEventListener('touchstart', e => {
        touchStartY = e.touches[0].clientY;
    }, {passive: true});
    document.addEventListener('touchend', e => {
        if (document.querySelector('.modal-overlay.active')) return;
        const dy = touchStartY - e.changedTouches[0].clientY;
        if (Math.abs(dy) > 50) {
            if (dy > 0) goToSlide(currentSlide+1);
            else goToSlide(currentSlide-1);
        }
    }, {passive: true});

    goToSlide(0);
})();

function openModal(id) {
    const m = document.getElementById(id);
    if (m) { m.classList.add('active'); document.body.style.overflow = 'hidden'; }
}
function closeModal(id) {
    const m = document.getElementById(id);
    if (m) { m.classList.remove('active'); document.body.style.overflow = ''; }
}

document.querySelectorAll('.modal-overlay').forEach(m => {
    m.addEventListener('click', e => {
        if (e.target === m) { m.classList.remove('active'); document.body.style.overflow = ''; }
    });
});

document.addEventListener('keydown', e => {
    if (e.key === 'Escape') {
        document.querySelectorAll('.modal-overlay.active').forEach(m => {
            m.classList.remove('active'); document.body.style.overflow = '';
        });
        document.getElementById('helpOverlay').classList.remove('active');
    }
});

document.getElementById('helpOverlay').addEventListener('click', e => {
    if (e.target === document.getElementById('helpOverlay'))
        e.target.classList.remove('active');
});
```

---

## 推荐幻灯片结构

不限页数，按项目实际需要增减。以下为推荐骨架：

| # | 幻灯片类型 | 内容 | 深度弹窗 |
|---|-----------|------|---------|
| 1 | 标题页 | 项目名、版本、一句话定位、技术标签 | 无 |
| 2 | 目录索引 | 可点击的页码跳转列表 | 无 |
| 3 | 技术要点总览 | 定位描述 + 三列技术矩阵 + 设计模式标签 | 可选 |
| 4 | 核心难点 | 6 个难点卡片 (2x3 网格) | 可选 |
| 5+ | 技术深潜 | 每个核心模块一页 (N 页) | **必须** |
| N-2 | 量化指标 | 统计卡片 + 部署架构图 | 可选 |
| N-1 | 技术决策 / Trade-offs | 选型对比、利弊分析 | 有 |
| N | 总结 | 架构全景回顾 + 统计标签 | 无 |

### 标题页模板

```html
<section class="slide gradient-bg grid-bg">
    <div class="slide-content" style="text-align:center;">
        <div class="logo">项目名称 <span>v1.0</span></div>
        <h1 style="background:linear-gradient(135deg,var(--accent),var(--accent-secondary));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;">一句话技术定位</h1>
        <p class="subtitle">技术标签 1 · 技术标签 2 · 技术标签 3</p>
        <p style="margin-top:1rem;">
            <span class="modal-tag">Pattern A</span>
            <span class="modal-tag">Pattern B</span>
        </p>
        <div class="meta">← → 翻页 · D 深度解析 · ? 快捷键</div>
    </div>
</section>
```

### 目录索引 (TOC) 模板

使用 `goToSlide(n)` 实现点击跳转（n 为 0-based 索引）：

```html
<section class="slide gradient-bg grid-bg">
    <div class="slide-content">
        <span class="section-label">TABLE OF CONTENTS</span>
        <h2>目录索引 <span style="font-size:0.5em;color:var(--text-secondary);font-weight:400;">(点击编号跳转)</span></h2>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.3rem 1.5rem;font-size:0.78em;">
            <div style="display:flex;gap:0.5rem;align-items:baseline;padding:0.2rem 0;border-bottom:1px solid rgba(255,255,255,0.06);cursor:pointer;" onclick="goToSlide(2)"><span style="color:var(--accent);font-family:'JetBrains Mono',monospace;min-width:1.5em;">3</span><span>技术概览</span></div>
            <div style="display:flex;gap:0.5rem;align-items:baseline;padding:0.2rem 0;border-bottom:1px solid rgba(255,255,255,0.06);cursor:pointer;" onclick="goToSlide(3)"><span style="color:var(--orange);font-family:'JetBrains Mono',monospace;min-width:1.5em;">4</span><span>核心难点</span></div>
            <!-- 更多条目... -->
        </div>
    </div>
</section>
```

TOC 编号颜色约定：概览类用 `var(--accent)` 绿色，核心模块用 `var(--orange)` 橙色，基础设施用 `var(--accent-secondary)` 蓝色，总结类用 `var(--text-secondary)` 灰色。

### 技术深潜页模板

```html
<section class="slide gradient-bg grid-bg">
    <div class="slide-content">
        <span class="section-label">MODULE NAME</span>
        <h2>模块标题</h2>
        <p style="margin-bottom:0.6rem;">一句话描述模块职责和核心价值</p>

        <div class="problem-box">
            <div class="problem-label">问题</div>
            <p>为什么需要这个模块</p>
        </div>

        <!-- 架构图 / 流程图 / 代码块 等组件 -->

        <div class="why-box">
            <div class="why-label">设计哲学</div>
            <p><strong>核心原则</strong> — 一句话总结设计思想</p>
        </div>
    </div>
    <button class="detail-btn" onclick="openModal('modal-xxx')">深度解析</button>
</section>
```

### 量化指标页模板

```html
<section class="slide gradient-bg grid-bg">
    <div class="slide-content">
        <span class="section-label">METRICS</span>
        <h2>量化指标</h2>
        <div class="stat-grid" style="margin-bottom:1.5rem;">
            <div class="stat-card"><div class="stat-number">数字</div><div class="stat-label">指标名</div></div>
            <div class="stat-card"><div class="stat-number orange">数字</div><div class="stat-label">指标名</div></div>
            <div class="stat-card"><div class="stat-number blue">数字</div><div class="stat-label">指标名</div></div>
        </div>
        <div class="arch-diagram">
            <!-- 部署架构层级图 -->
        </div>
    </div>
</section>
```

### 总结页模板

```html
<section class="slide gradient-bg grid-bg">
    <div class="slide-content" style="text-align:center;">
        <div class="logo">项目名称 <span>v1.0</span></div>
        <h1 style="background:linear-gradient(135deg,var(--accent),var(--accent-secondary));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;">Architecture Summary</h1>
        <div class="arch-diagram" style="text-align:left;margin:1rem auto;max-width:700px;">
            <!-- 全景架构回顾 -->
        </div>
        <p style="margin-top:1rem;">
            <span class="modal-tag">N Slides</span>
            <span class="modal-tag">M Deep Dives</span>
            <span class="modal-tag">K 代码片段</span>
        </p>
        <div class="meta">← → 翻页 · D 深度解析 · ? 快捷键</div>
    </div>
</section>
```

---

## 内容创建指南

### 整体叙事弧

| 阶段 | 幻灯片 | 目的 |
|------|--------|------|
| **定位** | 标题 + 目录 + 概览 | 建立项目全景，读者知道"这是什么" |
| **挑战** | 核心难点 | 展示项目解决的真实工程问题 |
| **深度** | 技术深潜 (N 页) | 逐模块深入：架构、实现、代码、设计模式 |
| **量化** | 指标 + 部署 | 用数据说明项目规模和能力 |
| **决策** | 技术决策 / Trade-offs | 为什么选 A 不选 B，权衡分析 |
| **演进** | 技术演进 | 版本历史、未来方向 |
| **收束** | 总结 | 全景回顾 + 统计 |

### 每页深潜的内容结构

1. **Section Label** — 全大写英文模块名
2. **标题** — 模块名 + 核心价值
3. **问题框** — 为什么需要这个模块
4. **架构图 / 流程图 / 代码块** — 可视化核心逻辑
5. **设计哲学框** — 一句话总结设计思想
6. **深度解析按钮** — 链接到对应弹窗

### 深度解析弹窗的内容结构

每个弹窗包含 3-6 个 `.modal-section`：

1. **核心概念** — 定义 + 为什么需要 + 与替代方案区别
2. **架构设计** — `.strategy-card` 展示组件和职责
3. **实现细节** — `.modal-code` 展示真实代码片段
4. **技术难点** — 难点 + 应对方案（可选）
5. **相关设计模式** — `.modal-tag` 标签 + `.modal-highlight` 一句话总结

---

## 使用流程

### Phase 1: 内容收集

1. 分析项目源码结构，识别核心模块
2. 提取每个模块的：核心概念、架构设计、关键代码、设计模式
3. 收集量化指标（代码行数、性能数据、模块数等）
4. 理解技术决策和 trade-offs

### Phase 2: 生成演示文稿

1. 按照推荐幻灯片结构组织内容
2. 使用完整的 CSS 变量和组件库
3. 为每个技术深潜页创建对应的深度解析弹窗
4. 包含完整的 Fixed Chrome 和 JavaScript

### Phase 3: 交付

提示用户：
- **← → 或滚轮** 切换幻灯片
- **D 或 Enter** 打开深度解析
- **ESC** 关闭弹窗
- **?** 查看所有快捷键
- **触摸设备** 上下滑动翻页

---

## 快速参考

| 组件 | 用途 | CSS 类 |
|------|------|--------|
| Section Label | 章节标记 | `.section-label` |
| 问题框 | 展示问题 | `.problem-box` |
| 方案框 | 展示方案 | `.solution-box` |
| 哲学框 | 设计理念 | `.why-box` |
| 流程节点 | 流程图 | `.flow-node` (+ `.active` `.success` `.warn` `.blue`) |
| 架构层 | 分层架构 | `.arch-layer` (+ `.orange` `.blue` `.purple`) |
| 代码块(幻灯片) | 代码展示 | `.code-block` |
| 代码块(弹窗) | 代码展示 | `.modal-code` |
| 统计卡 | 数字展示 | `.stat-card` / `.stat-number` (+ `.orange` `.blue`) |
| 技术标签 | 关键词 | `.modal-tag` |
| 深度按钮 | 打开弹窗 | `.detail-btn` |
| 进度条 | 顶部进度 | `.progress-bar` |
| 导航点 | 右侧导航 | `.nav-dot` |
| 页码 | 左下角 | `.slide-counter` |
| 帮助面板 | 快捷键 | `.help-overlay` |

---

## 完整示例

参考 `deerflow-presentation.html` (26 Slides + 20 Deep Dives)
