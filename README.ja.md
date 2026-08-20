[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md)

<div align="center">

# 🎨 Awesome Research Figures

**matplotlib のデフォルト設定ともう格闘しない。論文品質の科学図表を実現する 12 のスキル。**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#スキル一覧)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#ジャーナル仕様)

</div>

---

## スキル一覧

| # | カテゴリ | スキル | 説明 |
|---|----------|--------|------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | 出版品質の matplotlib 図表 |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | seaborn による統計可視化 |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | ネットワーク・グラフ可視化 |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | 機械学習結果の可視化 |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | 出版品質の ggplot2 図表 |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | バイオインフォマティクス可視化 |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | PGFPlots によるデータ可視化 |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | TikZ による技術図表 |
| 9 | 🔷 図表 | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | draw.io による技術図表 |
| 10 | 🔷 図表 | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | 手描き風図表 |
| 11 | 📐 フォーマット | [journal-specs](skills/期刊格式化/journal-specs.md) | ジャーナル図表仕様 |
| 12 | 📐 フォーマット | [figure-composition](skills/期刊格式化/figure-composition.md) | マルチパネル図表の構成 |

## クイックスタート

### Cursor

1. このリポジトリをプロジェクトまたは `~/.cursor/skills/` にクローン
2. Cursor を開くとスキルが自動検出されます
3. Cursor に入力：*"論文用の出版品質の混同行列を作成して"*

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

## ジャーナル仕様

| ジャーナル | シングルカラム | ダブルカラム | フォント | 最小サイズ |
|-----------|:------------:|:------------:|----------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

詳細は [journal-specs.md](skills/期刊格式化/journal-specs.md) を参照してください。

## 各スキルに含まれるもの

- **使用タイミング** — 明確なトリガー条件
- **ツールとライブラリ** — 正確なインストールコマンド
- **ステップバイステップの手順** — セットアップからエクスポートまで
- **コードテンプレート** — 実行可能な完成済みサンプル
- **スタイル仕様** — ジャーナル別のフォント、サイズ、カラー
- **よくある落とし穴** — 誰もがハマりやすいポイント
- **ジャーナル別ヒント** — IEEE、Nature、Science、Elsevier

## カラーパレット

すべてのスキルは [Wong (2011)](https://doi.org/10.1038/nmeth.1618) の色覚障害対応パレットを使用しています：

| 色 | カラーコード | 用途 |
|----|-------------|------|
| 🔵 青 | `#0072B2` | メイン / シリーズ 1 |
| 🟠 オレンジ | `#D55E00` | サブ / シリーズ 2 |
| 🟢 緑 | `#009E73` | サード / シリーズ 3 |
| 🩷 ピンク | `#CC79A7` | フォース / シリーズ 4 |
| 🟡 黄 | `#E69F00` | フィフス / シリーズ 5 |
| 🔷 水色 | `#56B4E9` | シリーズ 6 |

## 関連プロジェクト

- [awesome-skills](https://github.com/ai-era/awesome-skills) — AI エージェントスキルのキュレーションコレクション
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — デザイン・アート・メディア向けクリエイティブ AI スキル
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — AI コーディングアシスタントのルールとガイドライン
- [vibe-check](https://github.com/ai-era/vibe-check) — AI コード品質チェッカー
- [commit-ai](https://github.com/ai-era/commit-ai) — AI 搭載コミットメッセージジェネレーター
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Model Context Protocol サーバー
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — AI プロンプトキュレーションコレクション

---

## コントリビュート

コントリビューションを歓迎します！ガイドラインは [CONTRIBUTING.md](CONTRIBUTING.md) をご覧ください。

## ライセンス

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
