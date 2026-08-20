[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🎨 Awesome Research Figures

**توقف عن معاناة الإعدادات الافتراضية لـ matplotlib. 12 مهارة لإنشاء أشكال علمية بجودة النشر.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#skills)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#journal-specifications)

</div>

---

## قبل وبعد

**matplotlib الافتراضي** → **جاهز للنشر**

```
❌ matplotlib الافتراضي              ✅ مع awesome-research-figures
─────────────────────────────      ─────────────────────────────────
• خلفية رمادية قبيحة                • خلفية بيضاء نظيفة
• خطوط صغيرة غير مقروءة            • خطوط Times New Roman / Arial مناسبة
• ألوان أزرق/برتقالي افتراضية      • لوحات ألوان آمنة لضعاف البصر
• تصدير ضبابي بدقة 72 DPI          • PDF متجه حاد بدقة 600 DPI
• لا تنسيق للمحور                   • علامات تبويب نحو الداخل، حواف مناسبة
• تسميات متداخلة                     • ggrepel / adjustText
• حجم خاطئ للشكل                    • أبعاد IEEE/Nature/Science
```

---

## المهارات

| # | الفئة | المهارة | الوصف |
|---|----------|-------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | أشكال matplotlib بجودة النشر |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | تصور إحصائي باستخدام seaborn |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | تصور الشبكات والرسوم البيانية |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | تصور نتائج التعلم الآلي |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | أشكال ggplot2 بجودة النشر |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | تصور المعلومات الحيوية |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | تصور البيانات باستخدام PGFPlots |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | مخططات تقنية باستخدام TikZ |
| 9 | 🔷 مخططات | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | مخططات تقنية باستخدام draw.io |
| 10 | 🔷 مخططات | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | مخططات بأسلوب الرسم اليدوي |
| 11 | 📐 تنسيق | [journal-specs](skills/期刊格式化/journal-specs.md) | مواصفات أشكال المجلات |
| 12 | 📐 تنسيق | [figure-composition](skills/期刊格式化/figure-composition.md) | تكوين الأشكال متعددة اللوحات |

## البدء السريع

### Cursor

1. استنساخ هذا المستودع في مشروعك أو `~/.cursor/skills/`
2. افتح Cursor → يتم اكتشاف المهارات تلقائيًا
3. اسأل Cursor: *"أنشئ مصفوفة ارتباك بجودة النشر لورقتي البحثية"*

### Claude Code

```bash
# انسخ المهارات إلى دليل مهارات Claude Code الخاص بك
cp -r skills/ ~/.claude/skills/research-figures/
# أو أشر إليها في CLAUDE.md
echo "See ~/.claude/skills/research-figures/ for figure generation skills" >> CLAUDE.md
```

### Kimi Code

```bash
# يتم اكتشاف المهارات في .agents/skills/ تلقائيًا
mkdir -p .agents/skills/
cp -r skills/* .agents/skills/
```

## مواصفات المجلات

| المجلة | عمود واحد | عمودان | الخط | الحد الأدنى للحجم |
|---------|:------------:|:------------:|------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

راجع [journal-specs.md](skills/期刊格式化/journal-specs.md) للتفاصيل الكاملة.

## ما يوجد داخل كل مهارة

يتضمن كل ملف مهارة:

- **متى تستخدم** — شروط تشغيل واضحة
- **الأدوات والمكتبات** — أوامر التثبيت الدقيقة
- **تعليمات خطوة بخطوة** — من الإعداد إلى التصدير
- **قوالب الكود** — أمثلة كاملة وقابلة للتشغيل
- **مواصفات الأنماط** — الخطوط والأحجام والألوان لكل مجلة
- **المزالق الشائعة** — أشياء تسبب المشاكل للجميع
- **نصائح خاصة بالمجلات** — IEEE، Nature، Science، Elsevier

## لوحة الألوان

تستخدم جميع المهارات لوحة ألوان [Wong (2011)](https://doi.org/10.1038/nmeth.1618) الآمنة لضعاف البصر:

| اللون | Hex | الاستخدام |
|-------|-----|-----|
| 🔵 أزرق | `#0072B2` | أساسي / السلسلة 1 |
| 🟠 برتقالي | `#D55E00` | ثانوي / السلسلة 2 |
| 🟢 أخضر | `#009E73` | ثالثي / السلسلة 3 |
| 🩷 وردي | `#CC79A7` | رابعي / السلسلة 4 |
| 🟡 أصفر | `#E69F00` | خامسي / السلسلة 5 |
| 🔷 أزرق فاتح | `#56B4E9` | السلسلة 6 |

## انظر أيضًا

- [awesome-skills](https://github.com/ai-era/awesome-skills) — مجموعة منتقاة من مهارات الوكيل الذكي
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — مهارات الذكاء الاصطناعي الإبداعية للتصميم والفنون والوسائط
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — قواعد وإرشادات مساعد الترميز بالذكاء الاصطناعي
- [vibe-check](https://github.com/ai-era/vibe-check) — أداة فحص جودة كود الذكاء الاصطناعي
- [commit-ai](https://github.com/ai-era/commit-ai) — مولد رسائل الإيداع بالذكاء الاصطناعي
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — خوادم بروتوكول السياق النموذجي
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — مجموعة منتقاة من موجهات الذكاء الاصطناعي

---

## المساهمة

مرحب بالمساهمات! راجع [CONTRIBUTING.md](CONTRIBUTING.md) للإرشادات.

## الترخيص

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
