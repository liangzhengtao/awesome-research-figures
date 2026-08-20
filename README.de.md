[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🎨 Awesome Research Figures

**Schluss mit den Standard-Einstellungen von matplotlib. 12 Skills für wissenschaftliche Abbildungen in Publikationsqualität.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#skills)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#journal-specifications)

</div>

---

## Vorher & Nachher

**Standard-matplotlib** → **Publikationsbereit**

```
❌ Standard-matplotlib              ✅ Mit awesome-research-figures
─────────────────────────────      ─────────────────────────────────
• Hässlicher grauer Hintergrund     • Sauberer weißer Hintergrund
• Kleine unlesbare Schriften        • Passende Times New Roman / Arial
• Standard blaue/orange Farben      • Farbenblinden-sichere Paletten
• Unscharfer Export bei 72 DPI      • Scharfes Vektor-PDF bei 600 DPI
• Keine Achsenformatierung          • Innere Ticks, korrekte Rahmen
• Überlappende Beschriftungen       • ggrepel / adjustText
• Falsche Abbildungsgröße           • IEEE/Nature/Science-Maße
```

---

## Skills

| # | Kategorie | Skill | Beschreibung |
|---|----------|-------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | matplotlib-Abbildungen in Publikationsqualität |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | Statistische Visualisierung mit seaborn |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | Netzwerk- und Graphenvisualisierung |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | Visualisierung von Machine-Learning-Ergebnissen |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | ggplot2-Abbildungen in Publikationsqualität |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | Bioinformatik-Visualisierung |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | Datenvisualisierung mit PGFPlots |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | Technische Diagramme mit TikZ |
| 9 | 🔷 Diagramme | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | Technische Diagramme mit draw.io |
| 10 | 🔷 Diagramme | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | Handgezeichnete Diagramme |
| 11 | 📐 Formatierung | [journal-specs](skills/期刊格式化/journal-specs.md) | Abbildungsspezifikationen für Fachzeitschriften |
| 12 | 📐 Formatierung | [figure-composition](skills/期刊格式化/figure-composition.md) | Zusammensetzung von Mehrfachpanel-Abbildungen |

## Schnellstart

### Cursor

1. Klonen Sie dieses Repository in Ihr Projekt oder `~/.cursor/skills/`
2. Öffnen Sie Cursor → die Skills werden automatisch erkannt
3. Fragen Sie Cursor: *"Erstellen Sie eine Konfusionsmatrix in Publikationsqualität für meine Arbeit"*

### Claude Code

```bash
# Skills in das Claude Code Skill-Verzeichnis kopieren
cp -r skills/ ~/.claude/skills/research-figures/
# Oder in CLAUDE.md referenzieren
echo "See ~/.claude/skills/research-figures/ for figure generation skills" >> CLAUDE.md
```

### Kimi Code

```bash
# Skills in .agents/skills/ werden automatisch erkannt
mkdir -p .agents/skills/
cp -r skills/* .agents/skills/
```

## Fachzeitschriften-Spezifikationen

| Zeitschrift | Einfachspalte | Doppelspalte | Schriftart | Min. Größe |
|---------|:------------:|:------------:|------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

Alle Details finden Sie in [journal-specs.md](skills/期刊格式化/journal-specs.md).

## Was jeder Skill enthält

Jede Skill-Datei umfasst:

- **Wann verwenden** — klare Auslösebedingungen
- **Tools und Bibliotheken** — genaue Installationsbefehle
- **Schritt-für-Schritt-Anleitung** — von der Einrichtung bis zum Export
- **Code-Vorlagen** — vollständige, ausführbare Beispiele
- **Stilspezifikationen** — Schriftarten, Größen, Farben pro Zeitschrift
- **Häufige Fallstricke** — Fehler, die jedem unterlaufen
- **Zeitschriftenspezifische Tipps** — IEEE, Nature, Science, Elsevier

## Farbpalette

Alle Skills verwenden die farbenblinden-sichere Palette nach [Wong (2011)](https://doi.org/10.1038/nmeth.1618):

| Farbe | Hex | Verwendung |
|-------|-----|-----|
| 🔵 Blau | `#0072B2` | Primär / Serie 1 |
| 🟠 Orange | `#D55E00` | Sekundär / Serie 2 |
| 🟢 Grün | `#009E73` | Tertiär / Serie 3 |
| 🩷 Pink | `#CC79A7` | Quartär / Serie 4 |
| 🟡 Gelb | `#E69F00` | Quintär / Serie 5 |
| 🔷 Hellblau | `#56B4E9` | Serie 6 |

## Siehe auch

- [awesome-skills](https://github.com/ai-era/awesome-skills) — Kuratierte Sammlung von KI-Agent-Skills
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — Kreative KI-Skills für Design, Kunst und Medien
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — Regeln und Richtlinien für KI-Coding-Assistenten
- [vibe-check](https://github.com/ai-era/vibe-check) — KI-Codequalitätsprüfer
- [commit-ai](https://github.com/ai-era/commit-ai) — KI-gesteuerter Commit-Nachrichtengenerator
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Model Context Protocol Server
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — Kuratierte KI-Prompt-Sammlung

---

## Mitwirken

Beiträge sind willkommen! Siehe [CONTRIBUTING.md](CONTRIBUTING.md) für Richtlinien.

## Lizenz

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
