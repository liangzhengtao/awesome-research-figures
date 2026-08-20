[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Español](README.es.md) | [العربية](README.ar.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [Deutsch](README.de.md)

<div align="center">

# 🎨 Awesome Research Figures

**matplotlib 기본값과 씨름하지 마세요. 출판 수준의 과학 도형을 위한 12가지 스킬.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-12-orange.svg)](#skills)
[![Journals](https://img.shields.io/badge/Journals-IEEE%20%7C%20Nature%20%7C%20Science%20%7C%20Elsevier-green.svg)](#journal-specifications)

</div>

---

## Before & After

**기본 matplotlib** → **출판 준비 완료**

```
❌ 기본 matplotlib                  ✅ awesome-research-figures 사용
─────────────────────────────      ─────────────────────────────────
• 못생긴 회색 배경                   • 깔끔한 흰색 배경
• 작고 읽을 수 없는 폰트             • 적절한 Times New Roman / Arial
• 기본 파란/주황 색상                • 색각 이상 안전 팔레트
• 72 DPI 흐릿한 내보내기             • 600 DPI 선명한 벡터 PDF
• 축 포맷 없음                       • 안쪽 틱, 적절한 축 테두리
• 겹치는 레이블                      • ggrepel / adjustText
• 잘못된 그림 크기                   • IEEE/Nature/Science 규격
```

---

## 스킬 목록

| # | 카테고리 | 스킬 | 설명 |
|---|----------|-------|-------------|
| 1 | 🐍 Python | [matplotlib-publication](skills/Python绑图/matplotlib-publication.md) | 출판 수준의 matplotlib 도형 |
| 2 | 🐍 Python | [seaborn-statistical](skills/Python绑图/seaborn-statistical.md) | seaborn을 활용한 통계 시각화 |
| 3 | 🐍 Python | [network-graphs](skills/Python绑图/network-graphs.md) | 네트워크 및 그래프 시각화 |
| 4 | 🐍 Python | [ML-figures](skills/Python绑图/ML-figures.md) | 머신러닝 결과 시각화 |
| 5 | 📊 R | [ggplot2-publication](skills/R绑图/ggplot2-publication.md) | 출판 수준의 ggplot2 도형 |
| 6 | 📊 R | [bioinformatics-plots](skills/R绑图/bioinformatics-plots.md) | 생물정보학 시각화 |
| 7 | 📝 LaTeX | [pgfplots-charts](skills/LaTeX绑图/pgfplots-charts.md) | PGFPlots를 활용한 데이터 시각화 |
| 8 | 📝 LaTeX | [tikz-diagrams](skills/LaTeX绑图/tikz-diagrams.md) | TikZ를 활용한 기술 다이어그램 |
| 9 | 🔷 다이어그램 | [drawio-diagrams](skills/流程图与示意图/drawio-diagrams.md) | draw.io를 활용한 기술 다이어그램 |
| 10 | 🔷 다이어그램 | [excalidraw-sketches](skills/流程图与示意图/excalidraw-sketches.md) | 손그림 스타일 다이어그램 |
| 11 | 📐 포맷팅 | [journal-specs](skills/期刊格式化/journal-specs.md) | 저널 그림 규격 |
| 12 | 📐 포맷팅 | [figure-composition](skills/期刊格式化/figure-composition.md) | 다중 패널 그림 구성 |

## 빠른 시작

### Cursor

1. 이 저장소를 프로젝트나 `~/.cursor/skills/`에 클론하세요
2. Cursor를 열면 → 스킬이 자동으로 감지됩니다
3. Cursor에게 요청하세요: *"논문을 위한 출판 수준의 혼동 행렬을 만들어 주세요"*

### Claude Code

```bash
# 스킬을 Claude Code 스킬 디렉토리에 복사
cp -r skills/ ~/.claude/skills/research-figures/
# 또는 CLAUDE.md에 참조 추가
echo "See ~/.claude/skills/research-figures/ for figure generation skills" >> CLAUDE.md
```

### Kimi Code

```bash
# .agents/skills/의 스킬은 자동으로 감지됩니다
mkdir -p .agents/skills/
cp -r skills/* .agents/skills/
```

## 저널 규격

| 저널 | 단일 칼럼 | 이중 칼럼 | 폰트 | 최소 크기 |
|---------|:------------:|:------------:|------|:--------:|
| **IEEE** | 89 mm | 182 mm | Times New Roman | 6 pt |
| **Nature** | 89 mm | 183 mm | Arial | 6 pt |
| **Science** | 87 mm | 178 mm | Helvetica | 5 pt |
| **Elsevier** | 90 mm | 190 mm | Arial | 6 pt |
| **Springer** | 84 mm | 174 mm | Arial | 7 pt |
| **ACM** | 89 mm | 178 mm | Times/Helvetica | 6 pt |

자세한 내용은 [journal-specs.md](skills/期刊格式化/journal-specs.md)를 참조하세요.

## 각 스킬에 포함된 내용

각 스킬 파일에는 다음이 포함됩니다:

- **사용 시점** — 명확한 트리거 조건
- **도구 및 라이브러리** — 정확한 설치 명령어
- **단계별 안내** — 설정부터 내보내기까지
- **코드 템플릿** — 완전하고 실행 가능한 예제
- **스타일 규격** — 저널별 폰트, 크기, 색상
- **흔한 함정** — 누구나 빠지는 실수
- **저널별 팁** — IEEE, Nature, Science, Elsevier

## 색상 팔레트

모든 스킬은 [Wong (2011)](https://doi.org/10.1038/nmeth.1618) 색각 이상 안전 팔레트를 사용합니다:

| 색상 | Hex | 용도 |
|-------|-----|-----|
| 🔵 파랑 | `#0072B2` | 기본 / 시리즈 1 |
| 🟠 주황 | `#D55E00` | 보조 / 시리즈 2 |
| 🟢 초록 | `#009E73` | 삼차 / 시리즈 3 |
| 🩷 분홍 | `#CC79A7` | 사차 / 시리즈 4 |
| 🟡 노랑 | `#E69F00` | 오차 / 시리즈 5 |
| 🔷 하늘 | `#56B4E9` | 시리즈 6 |

## 함께 보기

- [awesome-skills](https://github.com/ai-era/awesome-skills) — AI 에이전트 스킬 큐레이션
- [awesome-creative-skills](https://github.com/ai-era/awesome-creative-skills) — 디자인, 예술, 미디어를 위한 크리에이티브 AI 스킬
- [awesome-ai-rules](https://github.com/ai-era/awesome-ai-rules) — AI 코딩 어시스턴트 규칙 및 가이드라인
- [vibe-check](https://github.com/ai-era/vibe-check) — AI 코드 품질 검사기
- [commit-ai](https://github.com/ai-era/commit-ai) — AI 기반 커밋 메시지 생성기
- [awesome-mcp-servers](https://github.com/ai-era/awesome-mcp-servers) — Model Context Protocol 서버
- [awesome-prompts](https://github.com/ai-era/awesome-prompts) — AI 프롬프트 큐레이션

---

## 기여

기여를 환영합니다! 가이드라인은 [CONTRIBUTING.md](CONTRIBUTING.md)를 참조하세요.

## 라이선스

[MIT](LICENSE) © [liangzhengtao](https://github.com/liangzhengtao)
