[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🎨 Awesome Research Figures

**Pare de lutar com os padrões do matplotlib. 12 habilidades para figuras científicas com qualidade de publicação.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#skills)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#journal-specifications)

</div>

---

## Antes & Depois

**matplotlib padrão** → **Pronto para publicação**

```
❌ matplotlib padrão                ✅ Com awesome-research-figures
─────────────────────────────      ─────────────────────────────────
• Fundo cinza feio                   • Fundo branco limpo
• Fontes pequenas ilegíveis          • Fontes Times New Roman / Arial adequadas
• Cores azul/laranja padrão          • Paletas seguras para daltônicos
• Exportação borrada em 72 DPI       • PDF vetorial nítido em 600 DPI
• Sem formatação dos eixos           • Marcas internas, bordas adequadas
• Rótulos sobrepostos                • ggrepel / adjustText
• Tamanho de figura incorreto        • Dimensões IEEE/Nature/Science
```

---

## Habilidades

| # | Categoria | Habilidade | Descrição |
|---|----------|-------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | Figuras matplotlib com qualidade de publicação |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | Visualização estatística com seaborn |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | Visualização de redes e grafos |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | Visualização de resultados de machine learning |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | Figuras ggplot2 com qualidade de publicação |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | Visualização bioinformática |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | Visualização de dados com PGFPlots |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | Diagramas técnicos com TikZ |
| 9 | 🔷 Diagramas | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | Diagramas técnicos com draw.io |
| 10 | 🔷 Diagramas | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | Diagramas estilo desenho à mão |
| 11 | 📐 Formatação | [journal-specs](skills/期刊格式化/journal-specs.md) | Especificações de figuras por periódico |
| 12 | 📐 Formatação | [figure-composition](skills/期刊格式化/figure-composition.md) | Composição de figuras multipainel |

## Início Rápido

### Cursor

1. Clone este repositório no seu projeto ou em `~/.cursor/skills/`
2. Abra o Cursor → as habilidades são detectadas automaticamente
3. Pergunte ao Cursor: *"Crie uma matriz de confusão com qualidade de publicação para meu artigo"*

### Claude Code

```bash
# Copie as habilidades para o diretório de habilidades do Claude Code
cp -r skills/ ~/.claude/skills/research-figures/
# Ou referencie no seu CLAUDE.md
echo "See ~/.claude/skills/research-figures/ for figure generation skills" >> CLAUDE.md
```

### Kimi Code

```bash
# Habilidades em .agents/skills/ são detectadas automaticamente
mkdir -p .agents/skills/
cp -r skills/* .agents/skills/
```

## Especificações de Periódicos

| Periódico | Coluna Simples | Coluna Dupla | Fonte | Tamanho Mínimo |
|---------|:------------:|:------------:|------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

Consulte [journal-specs.md](skills/期刊格式化/journal-specs.md) para detalhes completos.

## O Que Há em Cada Habilidade

Cada arquivo de habilidade inclui:

- **Quando Usar** — condições de acionamento claras
- **Ferramentas e Bibliotecas** — comandos de instalação exatos
- **Instruções Passo a Passo** — da configuração à exportação
- **Templates de Código** — exemplos completos e executáveis
- **Especificações de Estilo** — fontes, tamanhos, cores por periódico
- **Erros Comuns** — armadilhas que pegam todos
- **Dicas por Periódico** — IEEE, Nature, Science, Elsevier

## Paleta de Cores

Todas as habilidades usam a paleta segura para daltônicos [Wong (2011)](https://doi.org/10.1038/nmeth.1618):

| Cor | Hex | Uso |
|-------|-----|-----|
| 🔵 Azul | `#0072B2` | Primária / Série 1 |
| 🟠 Laranja | `#D55E00` | Secundária / Série 2 |
| 🟢 Verde | `#009E73` | Terciária / Série 3 |
| 🩷 Rosa | `#CC79A7` | Quaternária / Série 4 |
| 🟡 Amarelo | `#E69F00` | Quinária / Série 5 |
| 🔷 Azul Claro | `#56B4E9` | Série 6 |

## Veja Também

- [awesome-skills](https://github.com/ai-era/awesome-skills) — Coleção curada de habilidades para agentes de IA
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — Habilidades criativas de IA para design, arte e mídia
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — Regras e diretrizes para assistentes de código com IA
- [vibe-check](https://github.com/ai-era/vibe-check) — Verificador de qualidade de código com IA
- [commit-ai](https://github.com/ai-era/commit-ai) — Gerador de mensagens de commit com IA
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Servidores do Model Context Protocol
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — Coleção curada de prompts de IA

---

## Contribuição

Contribuições são bem-vindas! Consulte [CONTRIBUTING.md](CONTRIBUTING.md) para as diretrizes.

## Licença

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
