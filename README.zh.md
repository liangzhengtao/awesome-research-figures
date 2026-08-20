[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🎨 Awesome Research Figures

**别再和 matplotlib 默认样式较劲了。12 个技能，搞定学术论文级图表。**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#技能列表)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#期刊规范速查)

</div>

---

## 技能列表

| # | 分类 | 技能 | 说明 |
|---|------|------|------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | 出版级 matplotlib 图表 |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | 统计可视化 |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | 网络与图可视化 |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | 机器学习结果可视化 |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | 出版级 ggplot2 图表 |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | 生物信息学可视化 |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | PGFPlots 数据可视化 |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | TikZ 技术图表 |
| 9 | 🔷 图表 | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | draw.io 技术图表 |
| 10 | 🔷 图表 | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | 手绘风格图表 |
| 11 | 📐 格式化 | [journal-specs](skills/期刊格式化/journal-specs.md) | 期刊图表规范 |
| 12 | 📐 格式化 | [figure-composition](skills/期刊格式化/figure-composition.md) | 多面板图表组合 |

## 快速开始

### Cursor

1. 克隆本仓库到你的项目或 `~/.cursor/skills/`
2. 打开 Cursor → 技能自动识别
3. 输入：*"为我的论文创建一个出版级的混淆矩阵"*

### Claude Code

```bash
cp -r skills/ ~/.claude/skills/research-figures/
echo "See ~/.claude/skills/research-figures/ for figure generation skills" >> CLAUDE.md
```

### Kimi Code

```bash
mkdir -p .agents/skills/
cp -r skills/* .agents/skills/
```

## 期刊规范速查

| 期刊 | 单栏宽度 | 双栏宽度 | 字体 | 最小字号 |
|------|:--------:|:--------:|------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

## 每个技能包含

- **使用场景** — 明确的触发条件
- **工具和库** — 精确的安装命令
- **分步指南** — 从设置到导出
- **代码模板** — 完整可运行的示例
- **样式规范** — 各期刊的字体、字号、颜色
- **常见陷阱** — 每个人都会踩的坑
- **期刊技巧** — IEEE、Nature、Science、Elsevier

## 色板

所有技能使用 [Wong (2011)](https://doi.org/10.1038/nmeth.1618) 色盲友好色板：

| 颜色 | 色值 | 用途 |
|------|------|------|
| 🔵 蓝色 | `#0072B2` | 主色 / 系列 1 |
| 🟠 橙色 | `#D55E00` | 副色 / 系列 2 |
| 🟢 绿色 | `#009E73` | 第三色 / 系列 3 |
| 🩷 粉色 | `#CC79A7` | 第四色 / 系列 4 |
| 🟡 黄色 | `#E69F00` | 第五色 / 系列 5 |
| 🔷 浅蓝 | `#56B4E9` | 系列 6 |

## 相关项目

- [awesome-skills](https://github.com/ai-era/awesome-skills) — AI Agent 技能精选集合
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — 创意 AI 技能
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — AI 编码助手规则
- [vibe-check](https://github.com/ai-era/vibe-check) — AI 代码质量检查器
- [commit-ai](https://github.com/ai-era/commit-ai) — AI 提交信息生成器
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — MCP 服务器集合
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — AI 提示词精选

---

## 贡献

欢迎贡献！请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 了解指南。

## 许可证

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
