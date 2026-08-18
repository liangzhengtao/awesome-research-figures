[中文版](README.zh.md)

<div align="center">

# 🎨 Awesome Research Figures

**Stop wrestling with matplotlib defaults. 12 skills for publication-quality scientific figures.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#skills)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#journal-specifications)

</div>

---

## Before & After

**Default matplotlib** → **Publication-ready**

```
❌ Default matplotlib              ✅ With awesome-research-figures
─────────────────────────────      ─────────────────────────────────
• Ugly gray background             • Clean white background
• Tiny unreadable fonts             • Proper Times New Roman / Arial
• Default blue/orange colors        • Colorblind-safe palettes
• 72 DPI blurry export              • 600 DPI crisp vector PDF
• No axis formatting                • Inward ticks, proper spines
• Overlapping labels                • ggrepel / adjustText
• Wrong figure size                 • IEEE/Nature/Science dimensions
```

---

## Skills

| # | Category | Skill | Description |
|---|----------|-------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | Publication-quality matplotlib figures |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | Statistical visualization with seaborn |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | Network and graph visualization |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | Machine learning result visualization |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | Publication-quality ggplot2 figures |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | Bioinformatics visualization |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | Data visualization with PGFPlots |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | Technical diagrams with TikZ |
| 9 | 🔷 Diagrams | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | Technical diagrams with draw.io |
| 10 | 🔷 Diagrams | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | Hand-drawn style diagrams |
| 11 | 📐 Formatting | [journal-specs](skills/期刊格式化/journal-specs.md) | Journal figure specifications |
| 12 | 📐 Formatting | [figure-composition](skills/期刊格式化/figure-composition.md) | Multi-panel figure composition |

## Quick Start

### Cursor

1. Clone this repo into your project or `~/.cursor/skills/`
2. Open Cursor → the skills are auto-detected
3. Ask Cursor: *"Create a publication-quality confusion matrix for my paper"*

### Claude Code

```bash
# Copy skills to your Claude Code skills directory
cp -r skills/ ~/.claude/skills/research-figures/
# Or reference in your CLAUDE.md
echo "See ~/.claude/skills/research-figures/ for figure generation skills" >> CLAUDE.md
```

### Kimi Code

```bash
# Skills in .agents/skills/ are auto-detected
mkdir -p .agents/skills/
cp -r skills/* .agents/skills/
```

## Journal Specifications

| Journal | Single Column | Double Column | Font | Min Size |
|---------|:------------:|:------------:|------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

See [journal-specs.md](skills/期刊格式化/journal-specs.md) for complete details.

## What's Inside Each Skill

Each skill file includes:

- **When to Use** — clear trigger conditions
- **Tools and Libraries** — exact install commands
- **Step-by-step Instructions** — from setup to export
- **Code Templates** — complete, runnable examples
- **Style Specifications** — fonts, sizes, colors per journal
- **Common Pitfalls** — things that trip everyone up
- **Journal-Specific Tips** — IEEE, Nature, Science, Elsevier

## Color Palette

All skills use the [Wong (2011)](https://doi.org/10.1038/nmeth.1618) colorblind-safe palette:

| Color | Hex | Use |
|-------|-----|-----|
| 🔵 Blue | `#0072B2` | Primary / Series 1 |
| 🟠 Orange | `#D55E00` | Secondary / Series 2 |
| 🟢 Green | `#009E73` | Tertiary / Series 3 |
| 🩷 Pink | `#CC79A7` | Quaternary / Series 4 |
| 🟡 Yellow | `#E69F00` | Quinary / Series 5 |
| 🔷 Light Blue | `#56B4E9` | Series 6 |

## See Also

- [awesome-skills](https://github.com/ai-era/awesome-skills) — Curated collection of AI agent skills
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — Creative AI skills for design, art, and media
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — AI coding assistant rules and guidelines
- [vibe-check](https://github.com/ai-era/vibe-check) — AI code quality checker
- [commit-ai](https://github.com/ai-era/commit-ai) — AI-powered commit message generator
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Model Context Protocol servers
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — Curated AI prompts collection

---

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
