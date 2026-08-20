[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md)

<div align="center">

# 🎨 Awesome Research Figures

**Deja de pelear con los valores predeterminados de matplotlib. 12 habilidades para figuras científicas de calidad publicable.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#habilidades)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#especificaciones-de-revistas)

</div>

---

## Habilidades

| # | Categoría | Habilidad | Descripción |
|---|-----------|-----------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | Figuras matplotlib de calidad publicable |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | Visualización estadística con seaborn |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | Visualización de redes y grafos |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | Visualización de resultados de machine learning |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | Figuras ggplot2 de calidad publicable |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | Visualización en bioinformática |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | Visualización de datos con PGFPlots |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | Diagramas técnicos con TikZ |
| 9 | 🔷 Diagramas | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | Diagramas técnicos con draw.io |
| 10 | 🔷 Diagramas | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | Diagramas estilo dibujado a mano |
| 11 | 📐 Formato | [journal-specs](skills/期刊格式化/journal-specs.md) | Especificaciones de figuras por revista |
| 12 | 📐 Formato | [figure-composition](skills/期刊格式化/figure-composition.md) | Composición de figuras multipanel |

## Inicio rápido

### Cursor

1. Clona este repositorio en tu proyecto o en `~/.cursor/skills/`
2. Abre Cursor → las habilidades se detectan automáticamente
3. Pregunta a Cursor: *"Crea una matriz de confusión de calidad publicable para mi artículo"*

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

## Especificaciones de revistas

| Revista | Columna simple | Doble columna | Fuente | Tamaño mín. |
|---------|:--------------:|:--------------:|--------|:-----------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

Consulta [journal-specs.md](skills/期刊格式化/journal-specs.md) para todos los detalles.

## Contenido de cada habilidad

- **Cuándo usarla** — condiciones de activación claras
- **Herramientas y bibliotecas** — comandos de instalación exactos
- **Instrucciones paso a paso** — desde la configuración hasta la exportación
- **Plantillas de código** — ejemplos completos y ejecutables
- **Especificaciones de estilo** — fuentes, tamaños, colores por revista
- **Errores comunes** — problemas en los que todos tropiezan
- **Consejos por revista** — IEEE, Nature, Science, Elsevier

## Paleta de colores

Todas las habilidades usan la paleta accesible para daltonismo de [Wong (2011)](https://doi.org/10.1038/nmeth.1618) :

| Color | Hex | Uso |
|-------|-----|-----|
| 🔵 Azul | `#0072B2` | Principal / Serie 1 |
| 🟠 Naranja | `#D55E00` | Secundario / Serie 2 |
| 🟢 Verde | `#009E73` | Terciario / Serie 3 |
| 🩷 Rosa | `#CC79A7` | Cuaternario / Serie 4 |
| 🟡 Amarillo | `#E69F00` | Quinario / Serie 5 |
| 🔷 Azul claro | `#56B4E9` | Serie 6 |

## Ver también

- [awesome-skills](https://github.com/ai-era/awesome-skills) — Colección curada de habilidades para agentes IA
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — Habilidades IA creativas para diseño, arte y medios
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — Reglas y directrices para asistentes de codificación IA
- [vibe-check](https://github.com/ai-era/vibe-check) — Verificador de calidad de código IA
- [commit-ai](https://github.com/ai-era/commit-ai) — Generador de mensajes de commit con IA
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Servidores Model Context Protocol
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — Colección de prompts IA

---

## Contribuir

¡Las contribuciones son bienvenidas! Consulta [CONTRIBUTING.md](CONTRIBUTING.md) para las directrices.

## Licencia

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
