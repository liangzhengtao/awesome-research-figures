[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🎨 Awesome Research Figures

**Arrêtez de lutter contre les paramètres par défaut de matplotlib. 12 compétences pour des figures scientifiques de qualité publication.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#compétences)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#spécifications-des-revues)

</div>

---

## Compétences

| # | Catégorie | Compétence | Description |
|---|-----------|------------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | Figures matplotlib de qualité publication |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | Visualisation statistique avec seaborn |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | Visualisation de réseaux et graphes |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | Visualisation des résultats de machine learning |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | Figures ggplot2 de qualité publication |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | Visualisation en bioinformatique |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | Visualisation de données avec PGFPlots |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | Diagrammes techniques avec TikZ |
| 9 | 🔷 Diagrammes | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | Diagrammes techniques avec draw.io |
| 10 | 🔷 Diagrammes | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | Diagrammes de style dessiné à la main |
| 11 | 📐 Mise en forme | [journal-specs](skills/期刊格式化/journal-specs.md) | Spécifications des figures par revue |
| 12 | 📐 Mise en forme | [figure-composition](skills/期刊格式化/figure-composition.md) | Composition de figures multi-panneaux |

## Démarrage rapide

### Cursor

1. Clonez ce dépôt dans votre projet ou dans `~/.cursor/skills/`
2. Ouvrez Cursor → les compétences sont détectées automatiquement
3. Demandez à Cursor : *"Créez une matrice de confusion de qualité publication pour mon article"*

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

## Spécifications des revues

| Revue | Colonne simple | Double colonne | Police | Taille min. |
|-------|:--------------:|:--------------:|--------|:-----------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

Consultez [journal-specs.md](skills/期刊格式化/journal-specs.md) pour les détails complets.

## Contenu de chaque compétence

- **Quand l'utiliser** — conditions de déclenchement claires
- **Outils et bibliothèques** — commandes d'installation exactes
- **Instructions pas à pas** — de la configuration à l'exportation
- **Modèles de code** — exemples complets et exécutables
- **Spécifications de style** — polices, tailles, couleurs par revue
- **Pièges courants** — erreurs fréquentes à éviter
- **Conseils par revue** — IEEE, Nature, Science, Elsevier

## Palette de couleurs

Toutes les compétences utilisent la palette adaptée au daltonisme de [Wong (2011)](https://doi.org/10.1038/nmeth.1618) :

| Couleur | Hex | Utilisation |
|---------|-----|-------------|
| 🔵 Bleu | `#0072B2` | Principal / Série 1 |
| 🟠 Orange | `#D55E00` | Secondaire / Série 2 |
| 🟢 Vert | `#009E73` | Tertiaire / Série 3 |
| 🩷 Rose | `#CC79A7` | Quaternaire / Série 4 |
| 🟡 Jaune | `#E69F00` | Quinaire / Série 5 |
| 🔷 Bleu clair | `#56B4E9` | Série 6 |

## Voir aussi

- [awesome-skills](https://github.com/ai-era/awesome-skills) — Collection de compétences pour agents IA
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — Compétences IA créatives pour le design, l'art et les médias
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — Règles et directives pour assistants de codage IA
- [vibe-check](https://github.com/ai-era/vibe-check) — Vérificateur de qualité de code IA
- [commit-ai](https://github.com/ai-era/commit-ai) — Générateur de messages de commit par IA
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Serveurs Model Context Protocol
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — Collection de prompts IA

---

## Contribuer

Les contributions sont les bienvenues ! Consultez [CONTRIBUTING.md](CONTRIBUTING.md) pour les directives.

## Licence

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
