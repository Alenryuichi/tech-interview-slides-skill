# 🎯 Tech Interview Slides Skill

AI Skill for creating **high-density technical interview presentations** with **Neon Cyber** theme.

![Version](https://img.shields.io/badge/version-1.0.0-00ff88?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![Compatible](https://img.shields.io/badge/compatible-Claude%20Code%20%7C%20Augment-blueviolet?style=flat-square)

## ✨ Features

- **High Information Density** — Pack maximum technical content per slide
- **Deep-Dive Modals** — Click "📖 深度解析" to expand detailed explanations
- **Interview-Focused** — Every tech point has "面试加分点" tags
- **Zero Dependencies** — Single HTML file, inline CSS/JS
- **Viewport Fit** — Each slide fits 100dvh, responsive with `clamp()`

## 🎨 Preview

| Title Page | Challenge Cards | Architecture Diagram |
|------------|-----------------|---------------------|
| ![Title](https://via.placeholder.com/300x200/0a0a0f/00ff88?text=Title+Page) | ![Cards](https://via.placeholder.com/300x200/0a0a0f/fd6f32?text=Challenge+Cards) | ![Arch](https://via.placeholder.com/300x200/0a0a0f/00ccff?text=Architecture) |

## 📦 Installation

### Claude Code / Augment Code

```bash
# Clone to your skills directory
git clone https://github.com/Alenryuichi/tech-interview-slides-skill.git ~/.claude/skills/tech-interview-slides

# Or for Augment Code
git clone https://github.com/Alenryuichi/tech-interview-slides-skill.git ~/.augment/skills/tech-interview-slides
```

### Manual

1. Download `SKILL.md`
2. Place in one of these directories:
   - `~/.claude/skills/tech-interview-slides/SKILL.md`
   - `~/.augment/skills/tech-interview-slides/SKILL.md`
   - `<project>/.claude/skills/tech-interview-slides/SKILL.md`

## 🚀 Usage

Simply ask your AI assistant:

```
"帮我做一个技术面试的 PPT"
"Create a project presentation with architecture diagrams"
"做一个架构分享的演示文稿"
```

The skill will automatically trigger based on these keywords:
- 面试 PPT / interview slides
- 技术演示 / tech presentation
- 幻灯片 / slides / presentation
- 架构分享 / 项目展示

## 📐 Components

| Component | Purpose | CSS Class |
|-----------|---------|-----------|
| Section Label | Chapter markers | `.section-label` |
| Problem Box | Show problems (red) | `.problem-box` |
| Solution Box | Show solutions (green) | `.solution-box` |
| Why Box | Design philosophy | `.why-box` |
| Flow Node | Process diagrams | `.flow-node` |
| Arch Layer | Layered architecture | `.arch-layer` |
| Code Block | Syntax highlighting | `.code-block` |
| Stat Card | Metrics display | `.stat-card` |
| Modal Tag | Tech keywords | `.modal-tag` |
| Detail Button | Open deep-dive modal | `.detail-btn` |

## 🎯 Slide Structure (15 pages recommended)

| # | Type | Content |
|---|------|---------|
| 1 | Title | Project name, version, role |
| 2 | Overview | 3-column tech matrix |
| 3 | Challenges | 6 challenge cards (2×3 grid) |
| 4-9 | Deep Dive | One core module per page + modal |
| 10 | Case Study | Real debugging story |
| 11 | Metrics | Stats cards with numbers |
| 12 | Tech Decisions | Why you chose X over Y |
| 13 | Differentiation | Why hire you |
| 14 | Evolution | Future roadmap |
| 15 | Q&A | Thank you + contact |

## 🔗 Related

- [frontend-slides](https://github.com/Alenryuichi/frontend-slides-skill) — General presentation skill
- [frontend-design](https://github.com/Alenryuichi/frontend-design-skill) — Complex UI design

## 📄 License

MIT © 2026 TreeRen Chou

