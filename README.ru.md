[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🎨 Awesome Research Figures

**Хватит мучиться с настройками matplotlib по умолчанию. 12 навыков для создания научных фигур публикационного качества.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#skills)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#journal-specifications)

</div>

---

## До и После

**matplotlib по умолчанию** → **Готово к публикации**

```
❌ matplotlib по умолчанию          ✅ С awesome-research-figures
─────────────────────────────      ─────────────────────────────────
• Некрасивый серый фон               • Чистый белый фон
• Мелкий нечитаемый шрифт           • Корректный Times New Roman / Arial
• Стандартные синий/оранжевый цвета  • Палитра для людей с нарушением зрения
• Размытый экспорт 72 DPI           • Чёткий векторный PDF 600 DPI
• Нет форматирования осей            • Засечки внутрь, правильные рамки
• Перекрывающиеся подписи            • ggrepel / adjustText
• Неверный размер рисунка            • Размеры IEEE/Nature/Science
```

---

## Навыки

| # | Категория | Навык | Описание |
|---|----------|-------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | Фигуры matplotlib публикационного качества |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | Статистическая визуализация с seaborn |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | Визуализация сетей и графов |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | Визуализация результатов машинного обучения |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | Фигуры ggplot2 публикационного качества |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | Биоинформационная визуализация |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | Визуализация данных с PGFPlots |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | Технические диаграммы с TikZ |
| 9 | 🔷 Диаграммы | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | Технические диаграммы с draw.io |
| 10 | 🔷 Диаграммы | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | Диаграммы в стиле рисованных эскизов |
| 11 | 📐 Форматирование | [journal-specs](skills/期刊格式化/journal-specs.md) | Спецификации фигур для журналов |
| 12 | 📐 Форматирование | [figure-composition](skills/期刊格式化/figure-composition.md) | Составные фигуры из нескольких панелей |

## Быстрый старт

### Cursor

1. Клонируйте этот репозиторий в свой проект или в `~/.cursor/skills/`
2. Откройте Cursor → навыки определяются автоматически
3. Спросите Cursor: *"Создайте матрицу ошибок публикационного качества для моей статьи"*

### Claude Code

```bash
# Скопируйте навыки в каталог навыков Claude Code
cp -r skills/ ~/.claude/skills/research-figures/
# Или добавьте ссылку в CLAUDE.md
echo "See ~/.claude/skills/research-figures/ for figure generation skills" >> CLAUDE.md
```

### Kimi Code

```bash
# Навыки в .agents/skills/ определяются автоматически
mkdir -p .agents/skills/
cp -r skills/* .agents/skills/
```

## Спецификации журналов

| Журнал | Одна колонка | Две колонки | Шрифт | Мин. размер |
|---------|:------------:|:------------:|------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

Подробнее см. в [journal-specs.md](skills/期刊格式化/journal-specs.md).

## Что включает каждый навык

Каждый файл навыка содержит:

- **Когда использовать** — чёткие условия применения
- **Инструменты и библиотеки** — точные команды установки
- **Пошаговые инструкции** — от настройки до экспорта
- **Шаблоны кода** — полные рабочие примеры
- **Спецификации стиля** — шрифты, размеры, цвета для каждого журнала
- **Распространённые ошибки** — подводные камни, в которые попадают все
- **Советы для журналов** — IEEE, Nature, Science, Elsevier

## Цветовая палитра

Все навыки используют палитру [Wong (2011)](https://doi.org/10.1038/nmeth.1618), безопасную для людей с нарушением цветового зрения:

| Цвет | Hex | Использование |
|-------|-----|-----|
| 🔵 Синий | `#0072B2` | Основной / Серия 1 |
| 🟠 Оранжевый | `#D55E00` | Вторичный / Серия 2 |
| 🟢 Зелёный | `#009E73` | Третичный / Серия 3 |
| 🩷 Розовый | `#CC79A7` | Четвертичный / Серия 4 |
| 🟡 Жёлтый | `#E69F00` | Пятеричный / Серия 5 |
| 🔷 Голубой | `#56B4E9` | Серия 6 |

## Также смотрите

- [awesome-skills](https://github.com/ai-era/awesome-skills) — Коллекция навыков ИИ-агентов
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — Креативные навыки ИИ для дизайна, искусства и медиа
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — Правила и руководства для ИИ-ассистентов кодирования
- [vibe-check](https://github.com/ai-era/vibe-check) — Проверка качества кода с помощью ИИ
- [commit-ai](https://github.com/ai-era/commit-ai) — Генератор сообщений коммитов на основе ИИ
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Серверы Model Context Protocol
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — Коллекция ИИ-промптов

---

## Участие

Приветствуются вклады! Смотрите [CONTRIBUTING.md](CONTRIBUTING.md) для руководства.

## Лицензия

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
