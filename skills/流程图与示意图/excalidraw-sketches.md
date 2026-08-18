# Hand-Drawn Style Diagrams with Excalidraw

## When to Use

- Creating informal, approachable diagrams for presentations or blogs
- Building concept maps, process diagrams, or architecture sketches
- Need a "hand-drawn" aesthetic for educational or outreach materials
- Collaborative diagramming with real-time editing
- Quick visual brainstorming for research ideas

## Tools and Libraries

- [Excalidraw](https://excalidraw.com/) (web app, self-hosted, or VS Code extension)
- `@excalidraw/excalidraw` npm package for embedding
- VS Code extension: `pomdtr.excalidraw-editor`

## Step-by-Step Instructions

### 1. Setting Up Excalidraw

**Web app**: Navigate to https://excalidraw.com/
**VS Code**: Install `pomdtr.excalidraw-editor` extension
**Self-hosted**: `npx @excalidraw/excalidraw`

### 2. Configure for Publications

1. **Canvas settings**: Click the canvas background → set to white (#FFFFFF)
2. **Grid**: Toggle grid on (Ctrl+G) for alignment
3. **Font**: Excalidraw uses Virgil (hand-drawn) by default; switch to "Normal" for publications
4. **Export settings**: Export as SVG for vector quality

### 3. Color Palette for Academic Use

```
Primary Blue:    #1971c2
Primary Green:    #2f9e44
Primary Orange:   #e8590c
Accent Purple:    #7048e8
Accent Pink:      #c2255c
Text Black:       #1e1e1e
Background:       #ffffff
```

## Code Templates

### Template 1: Concept Map

```
Excalidraw JSON structure for a concept map:

Central concept: "Machine Learning"
  ├── Supervised Learning
  │   ├── Classification
  │   └── Regression
  ├── Unsupervised Learning
  │   ├── Clustering
  │   └── Dimensionality Reduction
  └── Reinforcement Learning
      ├── Policy Gradient
      └── Q-Learning

Steps to create:
1. Create a rectangle for "Machine Learning" (center, blue fill)
2. Create rectangles for each subcategory
3. Connect with arrow elements
4. Add text labels to arrows (e.g., "includes", "uses")
5. Use color coding: blue for main, green for supervised,
   orange for unsupervised, purple for reinforcement
```

### Template 2: Process / Workflow Diagram

```
Process diagram layout:

[Problem Definition]
       ↓ (arrow)
[Data Collection]
       ↓
[Preprocessing] ──→ [Feature Engineering]
       ↓                    ↓
[Model Selection]  ←───────┘
       ↓
[Training & Validation]
       ↓
[Evaluation Metrics]
       ↓
  ┌────┴────┐
[Pass]    [Fail] ──→ [Hyperparameter Tuning] ──→ [Training]
  ↓
[Deployment]

Excalidraw tips:
- Use rectangles for processes, diamonds for decisions
- Set strokeStyle="dashed" for feedback loops
- Group related elements (Ctrl+G) for easy movement
- Use "Arrow" tool with rounded style for connections
```

### Template 3: Architecture Sketch

```
Layered architecture sketch:

┌─────────────────────────────────┐
│         Frontend Layer          │  ← Rectangle, light blue fill
│  ┌───────┐  ┌───────┐  ┌────┐  │
│  │  Web  │  │Mobile │  │ CLI│  │  ← Sub-rectangles
│  └───────┘  └───────┘  └────┘  │
└─────────────────────────────────┘
               ↕                    ← Bidirectional arrow
┌─────────────────────────────────┐
│       API Gateway Layer         │  ← Light green fill
│  ┌──────────┐  ┌─────────────┐  │
│  │   REST   │  │  GraphQL    │  │
│  └──────────┘  └─────────────┘  │
└─────────────────────────────────┘
               ↕
┌─────────────────────────────────┐
│       Service Layer             │  ← Light orange fill
│  ┌────┐ ┌────┐ ┌─────┐ ┌─────┐│
│  │Auth│ │Core│ │ ML  │ │ Notif││
│  └────┘ └────┘ └─────┘ └─────┘│
└─────────────────────────────────┘
               ↕
┌─────────────────────────────────┐
│        Data Layer               │  ← Light purple fill
│  ┌────┐  ┌─────┐  ┌──────────┐ │
│  │ SQL│  │Redis│  │S3 / Files│ │
│  └────┘  └─────┘  └──────────┘ │
└─────────────────────────────────┘
```

### Template 4: Research Methodology Diagram

```
Methodology flow diagram (for paper methodology section):

    ┌──────────────┐
    │ Research     │
    │ Questions    │
    └──────┬───────┘
           ↓
    ┌──────────────┐     ┌──────────────┐
    │ Data         │────→│ Ground Truth │
    │ Collection   │     │ Annotation   │
    └──────┬───────┘     └──────┬───────┘
           ↓                    ↓
    ┌──────────────┐     ┌──────────────┐
    │ Proposed     │     │ Evaluation   │
    │ Method       │────→│ Metrics      │
    └──────┬───────┘     └──────┬───────┘
           ↓                    ↓
    ┌──────────────┐     ┌──────────────┐
    │ Baseline     │     │ Statistical  │
    │ Comparison   │────→│ Analysis     │
    └──────────────┘     └──────────────┘
```

## Export Settings for Publications

### SVG Export (Recommended)
```
Export → SVG
  - Background: White
  - Scale: 2x (for high DPI)
  - Embed fonts: checked
```

### PNG Export
```
Export → PNG
  - Scale: 3x (for 300 DPI at standard figure size)
  - Background: White (transparent off)
```

### Import into LaTeX
```latex
\usepackage{svg}
% Or convert SVG to PDF first:
% inkscape input.svg --export-pdf=output.pdf
\includegraphics[width=\columnwidth]{diagram.pdf}
```

## Style Specifications

| Element | Property | Value |
|---------|----------|-------|
| Background | color | #FFFFFF (white for print) |
| Stroke style | Roughness | 1 (architect) or 2 (artist) |
| Stroke width | strokeWidth | 2 (normal) |
| Font | fontFamily | 1 (Virgil/hand-drawn) or 2 (Helvetica/clean) |
| Font size | fontSize | 20 (default) or 16 (small) |
| Fill | backgroundColor | Pastel colors with 15-30% opacity |
| Grid | showGrid | true (for alignment) |
| Roundness | roundness | true for rectangles |

## Common Pitfalls

1. **Hand-drawn font unreadable at small sizes**: Switch to "Normal" font for sizes < 14 pt
2. **Export resolution too low**: Use 2x or 3x scale for print
3. **Background not white**: Set white background before export for papers
4. **SVG text not editable in LaTeX**: Convert SVG → PDF via Inkscape
5. **Alignment issues**: Use grid snapping (Ctrl+G) and alignment tools
6. **File format**: Save as `.excalidraw` (JSON) for re-editing, export as SVG/PDF for papers
7. **Collaboration links expire**: Export and version control important diagrams

## Journal-Specific Tips

- **Nature/Science**: Prefer clean professional look; use "Normal" font mode
- **IEEE**: Convert to PDF/SVG; hand-drawn style acceptable for conceptual diagrams
- **Blog posts**: Excalidraw's default style is ideal for educational content
- **Presentations**: Use PNG at 3x scale; pair with hand-drawn slide templates
- **Thesis**: Use Excalidraw for initial sketches, refine to TikZ for final version
- **General**: Excalidraw stores state as JSON — version control your `.excalidraw` files

---

## 中文版本

### 使用场景
- 为演示文稿或博客创建非正式、平易近人的图表
- 构建概念图、流程图或架构草图
- 教育或科普材料需要"手绘"美学
- 实时协作编辑图表
- 研究想法的快速视觉头脑风暴

### 工具库
- [Excalidraw](https://excalidraw.com/)（网页版、自托管或 VS Code 扩展）
- `@excalidraw/excalidraw` npm 包用于嵌入
- VS Code 扩展：`pomdtr.excalidraw-editor`

### 代码模板说明
- **概念图**：中心节点+分支结构，按类别颜色编码（蓝=主、绿=监督、橙=无监督、紫=强化）
- **流程图**：矩形=处理、菱形=判断、虚线=反馈回路，使用 Ctrl+G 分组
- **架构草图**：分层架构（前端→API 网关→服务层→数据层），每层不同颜色
- **研究方法论图**：问题定义→数据收集→方法→评估→统计分析

### 导出设置
- **SVG（推荐）**：白色背景，2x 缩放，嵌入字体
- **PNG**：3x 缩放（标准尺寸下 300 DPI），白色背景
- **LaTeX 导入**：`\usepackage{svg}` 或 Inkscape 转 PDF 后 `\includegraphics`

### 常见陷阱
1. **手绘字体在小尺寸下不可读**：字号 < 14 pt 时切换为"Normal"字体
2. **导出分辨率过低**：印刷用 2x 或 3x 缩放
3. **背景非白色**：导出前设置白色背景用于论文
4. **SVG 文本在 LaTeX 中不可编辑**：通过 Inkscape 将 SVG → PDF
5. **对齐问题**：使用网格吸附（Ctrl+G）和对齐工具
6. **文件格式**：保存为 `.excalidraw`（JSON）便于再编辑，导出 SVG/PDF 用于论文
7. **协作链接过期**：导出并对重要图表进行版本控制
