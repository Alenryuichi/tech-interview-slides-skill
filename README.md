# 🔬 Tech Deep-Dive Slides Skill

AI Skill for creating **high-density technical deep-dive presentations** with **Neon Cyber** dark theme. Turn any project, paper, or codebase into an interactive single-file HTML presentation with deep-dive modals.

![Version](https://img.shields.io/badge/version-2.0.0-00ff88?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![Compatible](https://img.shields.io/badge/compatible-Claude%20Code%20%7C%20Augment%20%7C%20Cursor-blueviolet?style=flat-square)

> **v2.0 Breaking Change:** Rebranded from interview-focused to general-purpose technical deep-dive. See [v1.0.0](https://github.com/Alenryuichi/tech-interview-slides-skill/tree/v1.0.0) for the original interview version.

## What's New in v2.0

| Feature | v1.0 (Interview) | v2.0 (Deep Dive) |
|---------|-------------------|-------------------|
| **Positioning** | Interview prep | Any technical project analysis |
| **Fixed Chrome** | None | Progress bar, nav dots, slide counter, help overlay |
| **Navigation** | Arrow keys only | Keyboard + wheel + touch/swipe + `?` help |
| **Deep Dive Shortcut** | Click only | `Enter` / `D` key |
| **Slide Types** | 15 fixed slides | Flexible: Title → TOC → N Deep Dives → Metrics → Summary |
| **TOC** | None | Clickable `goToSlide()` index |
| **Print** | None | `@media print` stylesheet |
| **CSS Animations** | None | Slide enter + pulse + modal scale |
| **Color Variants** | Green + Orange | Green + Orange + Blue + Purple |

## Features

- **High Information Density** — Slides packed with architecture diagrams, flow charts, code blocks, and stat cards
- **Deep-Dive Modals** — Every technical slide has a "📖 深度解析" button expanding into detailed analysis with code, strategy cards, and design pattern tags
- **Fixed Chrome UI** — Progress bar (top), navigation dots (right), slide counter (bottom-left), keyboard help overlay
- **Full Navigation** — Arrow keys, Space, Page Up/Down, Home/End, scroll wheel, touch swipe
- **Zero Dependencies** — Single HTML file, inline CSS/JS, only external link is Fontshare fonts
- **Responsive** — `clamp()` sizing, `100dvh` slides, mobile nav dots
- **Print-Friendly** — `@media print` stylesheet renders slides and modals as pages

## Installation

### Claude Code / Augment Code / Cursor

```bash
# Clone to your skills directory
git clone https://github.com/Alenryuichi/tech-interview-slides-skill.git ~/.claude/skills/tech-interview-slides

# Or for Cursor
git clone https://github.com/Alenryuichi/tech-interview-slides-skill.git <project>/.claude/skills/tech-interview-slides
```

### Manual

1. Download `tech-interview-slides/SKILL.md`
2. Place in: `~/.claude/skills/tech-interview-slides/SKILL.md`

## Usage

Ask your AI assistant:

```
"帮我做一个技术深度解析的 PPT"
"分析这个开源项目，生成 PPT"
"Create a technical deep-dive presentation for this project"
"做一个架构分享的演示文稿"
```

Triggers: `技术 PPT`, `技术演示`, `presentation`, `slides`, `幻灯片`, `架构分享`, `项目展示`, `tech presentation`, `技术深度解析`, `开源项目解析`

## Components

| Component | Purpose | CSS Class | Variants |
|-----------|---------|-----------|----------|
| Section Label | Chapter marker with pulse dot | `.section-label` | — |
| Problem Box | Show problems (red) | `.problem-box` | — |
| Solution Box | Show solutions (green) | `.solution-box` | — |
| Why Box | Design philosophy (accent) | `.why-box` | — |
| Flow Node | Process flow diagrams | `.flow-node` | `.active` `.success` `.warn` `.blue` |
| Arch Layer | Layered architecture | `.arch-layer` | `.orange` `.blue` `.purple` |
| Code Block | Syntax-highlighted code (slides) | `.code-block` | — |
| Modal Code | Code in deep-dive modals | `.modal-code` | — |
| Stat Card | Metrics display | `.stat-card` | `.stat-number.orange` `.blue` |
| Modal Tag | Design pattern labels | `.modal-tag` | — |
| Strategy Card | Component analysis (modals) | `.strategy-card` | — |
| Modal Highlight | Key insight callout (modals) | `.modal-highlight` | — |
| Detail Button | Open deep-dive modal | `.detail-btn` | — |
| Progress Bar | Top reading progress | `.progress-bar` | — |
| Nav Dots | Right-side slide navigation | `.nav-dot` | `.active` |
| Slide Counter | Bottom-left page number | `.slide-counter` | — |
| Help Overlay | Keyboard shortcut reference | `.help-overlay` | — |

## Recommended Slide Structure

Flexible — add as many deep-dive pages as needed:

| # | Type | Content | Modal |
|---|------|---------|-------|
| 1 | Title | Project name, version, tech tags | — |
| 2 | TOC | Clickable `goToSlide()` index | — |
| 3 | Overview | Architecture pillars, design patterns | Optional |
| 4 | Challenges | 6 challenge cards (2×3) | Optional |
| 5+ | Deep Dive | One module per page (N pages) | **Required** |
| N-2 | Metrics | Stat cards + deployment arch | Optional |
| N-1 | Trade-offs | Decision tables, pros/cons | Yes |
| N | Summary | Architecture panorama + tags | — |

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `→` `↓` `Space` `PageDown` | Next slide |
| `←` `↑` `PageUp` | Previous slide |
| `Home` / `End` | First / Last slide |
| `Enter` / `D` | Open deep-dive modal |
| `Esc` | Close modal / help |
| `?` | Toggle help overlay |

Touch: swipe up/down to navigate.

## Example Output

See the [autoresearch-presentation.html](https://github.com/Alenryuichi/tech-interview-slides-skill/blob/main/examples/autoresearch-presentation.html) — a 14-slide + 10 deep-dive presentation generated for [karpathy/autoresearch](https://github.com/karpathy/autoresearch) using this skill.

## Changelog

### v2.0.0 (2026-03-27)

- **BREAKING:** Rebranded from interview-focused to general-purpose technical deep-dive
- Added Fixed Chrome UI (progress bar, nav dots, slide counter, help overlay)
- Added complete JavaScript IIFE (keyboard, wheel, touch, `goToSlide`, `Enter`/`D` shortcut)
- Added slide types: TOC, Metrics, Trade-offs, Summary templates
- Added CSS: slide enter animation, pulse keyframes, `.blue`/`.purple` variants, print stylesheet
- Added `.modal-code` (distinct from `.code-block`), `.strategy-card`, `.modal-highlight`
- Replaced interview content guide with flexible technical deep-dive structure
- Removed all interview-specific content (面试加分点, 面试话术)

### v1.0.0 (2026-03-26)

- Initial release: Interview-focused tech slides with Neon Cyber theme

## License

MIT © 2026 TreeRen Chou
