# Journal Figure Specifications

## When to Use

- Formatting figures for a specific journal (IEEE, ACM, Nature, Science, Elsevier, Springer)
- Checking figure dimensions, resolution, font requirements before submission
- Preparing a figure compliance checklist
- Converting figures between journal format requirements
- Verifying color mode and file format requirements

## Tools and Libraries

```
pip install Pillow        # Image processing and DPI verification
pip install matplotlib    # For PDF/EPS generation
```

```bash
# CLI tools for verification
brew install imagemagick   # macOS
apt install imagemagick    # Linux
# Windows: download from imagemagick.org
```

## Step-by-Step Instructions

### 1. Figure Compliance Checklist

Before submitting, verify each figure against:

```
□ Dimensions match journal specifications
□ Resolution meets minimum (300 DPI raster, 600+ DPI line art)
□ Font family matches journal requirements
□ Font size ≥ minimum (usually 5-6 pt at final size)
□ Color mode correct (RGB for screen, CMYK for print)
□ File format accepted by journal
□ Line width ≥ minimum (usually 0.5 pt)
□ All text is legible at final print size
□ Figure number and caption not embedded in image
□ No embedded metadata or layers that may cause issues
```

### 2. DPI Verification Script

```python
from PIL import Image
import os

def check_dpi(filepath, min_dpi=300):
    """Check if image meets DPI requirements."""
    if filepath.lower().endswith(('.pdf', '.eps', '.svg')):
        print(f"  {filepath}: Vector format, DPI not applicable ✓")
        return True

    img = Image.open(filepath)
    dpi = img.info.get('dpi', (72, 72))
    dpi_x, dpi_y = dpi[0], dpi[1] if len(dpi) > 1 else dpi[0]

    w, h = img.size
    status = "✓" if dpi_x >= min_dpi else "✗"
    print(f"  {filepath}: {w}x{h} @ {dpi_x:.0f} DPI {status}")

    if dpi_x < min_dpi:
        needed_w = int(w * min_dpi / dpi_x)
        needed_h = int(h * min_dpi / dpi_y)
        print(f"    → Re-export at {needed_w}x{needed_h} pixels minimum")
    return dpi_x >= min_dpi

# Usage
for f in os.listdir('figures'):
    if f.endswith(('.png', '.jpg', '.tiff')):
        check_dpi(os.path.join('figures', f), min_dpi=300)
```

## Code Templates

### Template 1: Figure Size Verification

```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

def check_figure_size(filepath, target_width_inch, target_height_inch):
    """Verify figure dimensions match journal requirements."""
    if filepath.lower().endswith(('.pdf', '.eps')):
        from matplotlib.backends.backend_pdf import PdfPages
        print(f"  PDF/EPS detected — check dimensions in viewer")
        print(f"  Target: {target_width_inch} x {target_height_inch} inches")
        return

    img = mpimg.imread(filepath)
    h_px, w_px = img.shape[:2]
    dpi = 300  # assume target DPI

    actual_w = w_px / dpi
    actual_h = h_px / dpi

    print(f"  {filepath}:")
    print(f"    Actual:   {actual_w:.2f} x {actual_h:.2f} inches @ {dpi} DPI")
    print(f"    Target:   {target_width_inch:.2f} x {target_height_inch:.2f} inches")
    print(f"    Pixels:   {w_px} x {h_px}")

    if abs(actual_w - target_width_inch) > 0.1:
        print(f"    ⚠ Width mismatch: resize to {int(target_width_inch * dpi)} px")
```

## Journal Specifications Reference

### IEEE

| Property | Single Column | Double Column |
|----------|--------------|---------------|
| Width | 89 mm (3.5 in) | 182 mm (7.16 in) |
| Max height | 230 mm (9.06 in) | 230 mm (9.06 in) |
| Font | Times New Roman | Times New Roman |
| Min font size | 6 pt | 6 pt |
| Resolution (color) | 300 dpi | 300 dpi |
| Resolution (line art) | 600 dpi | 600 dpi |
| Color mode | RGB | RGB |
| Formats | EPS, PDF, TIFF, PNG | EPS, PDF, TIFF, PNG |
| Line width (min) | 0.5 pt | 0.5 pt |

**LaTeX template**:
```latex
\documentclass[journal]{IEEEtran}
\usepackage{graphicx}
\begin{figure}[t]
  \centering
  \includegraphics[width=\columnwidth]{fig1.pdf}
  \caption{Figure caption here.}\label{fig:example}
\end{figure}
```

### Nature

| Property | Single Column | Double Column |
|----------|--------------|---------------|
| Width | 89 mm (3.5 in) | 183 mm (7.2 in) |
| Max height | 247 mm (9.72 in) | 247 mm (9.72 in) |
| Font | Arial / Helvetica | Arial / Helvetica |
| Min font size | 6 pt (5 pt acceptable) | 6 pt (5 pt acceptable) |
| Resolution | 300 dpi | 300 dpi |
| Resolution (line art) | 1000 dpi | 1000 dpi |
| Color mode | RGB | RGB |
| Formats | PDF, EPS, TIFF, PNG | PDF, EPS, TIFF, PNG |
| Max file size | 10 MB | 10 MB |

**Special requirements**:
- Provide source data for all figures
- Figure files should be separate from manuscript
- Maximum 8 display items (figures + tables)

### Science

| Property | Single Column | Double Column |
|----------|--------------|---------------|
| Width | 87 mm (3.42 in) | 178 mm (7.0 in) |
| Max height | 240 mm (9.45 in) | 240 mm (9.45 in) |
| Font | Helvetica / Arial | Helvetica / Arial |
| Min font size | 5 pt | 5 pt |
| Resolution | 300 dpi | 300 dpi |
| Color mode | RGB | RGB |
| Formats | PDF, EPS, TIFF, PNG | PDF, EPS, TIFF, PNG |

### Elsevier

| Property | Single Column | Double Column |
|----------|--------------|---------------|
| Width | 90 mm (3.54 in) | 190 mm (7.48 in) |
| Max height | 240 mm | 240 mm |
| Font | Arial, Helvetica, Courier | Arial, Helvetica, Courier |
| Min font size | 6 pt | 6 pt |
| Resolution (color) | 300 dpi | 300 dpi |
| Resolution (line art) | 1000 dpi | 1000 dpi |
| Color mode | CMYK preferred | CMYK preferred |
| Formats | EPS, PDF, TIFF, JPG, PNG | EPS, PDF, TIFF, JPG, PNG |

### Springer

| Property | Single Column | Double Column |
|----------|--------------|---------------|
| Width | 84 mm (3.31 in) | 174 mm (6.85 in) |
| Max height | 234 mm | 234 mm |
| Font | Arial, Helvetica | Arial, Helvetica |
| Min font size | 7 pt | 7 pt |
| Resolution (color) | 300 dpi | 300 dpi |
| Resolution (line art) | 1200 dpi | 1200 dpi |
| Color mode | RGB | RGB (CMYK for print) |
| Formats | EPS, PDF, TIFF, PNG | EPS, PDF, TIFF, PNG |

### ACM

| Property | Single Column | Double Column |
|----------|--------------|---------------|
| Width | 89 mm (3.5 in) | 178 mm (7.0 in) |
| Max height | 230 mm | 230 mm |
| Font | Times New Roman, Helvetica | Times New Roman, Helvetica |
| Min font size | 6 pt | 6 pt |
| Resolution | 300 dpi | 300 dpi |
| Formats | EPS, PDF, TIFF, PNG | EPS, PDF, TIFF, PNG |

### PLOS ONE

| Property | Value |
|----------|-------|
| Width | 77.5 mm (single) to 172 mm (full) |
| Resolution | 300 dpi minimum |
| Formats | TIFF, EPS, PDF |
| Font | Arial, Helvetica |
| Min font size | 8 pt |
| Color mode | RGB |

## Common Pitfalls

1. **DPI confused with PPI**: DPI is for print; PPI is for screens. Journals mean DPI for print quality
2. **Vector formats have no DPI**: PDF/EPS/SVG are resolution-independent; DPI only applies to raster
3. **Font size changes on resize**: Always check font size at final print dimensions
4. **CMYK color shift**: Convert from RGB to CMYK only if journal requires it; colors may shift
5. **TIFF compression**: Use LZW compression for TIFF; avoid JPEG compression in TIFF
6. **PDF version**: PDF 1.4+ recommended; avoid PDF 2.0 features
7. **Embedded fonts in PDF**: Ensure all fonts are embedded (use `pdffonts` to check)

## Common Conversion Commands

```bash
# PNG to TIFF with DPI
convert input.png -density 300 -units PixelsPerInch output.tiff

# PDF to high-res PNG
convert -density 600 input.pdf output.png

# RGB to CMYK (requires ICC profile)
convert input.png -profile sRGB.icc -profile CMYK.icc output.tiff

# Check PDF fonts
pdffonts input.pdf

# Resize to target width (pixels)
convert input.png -resize 2100x output.png  # 7 inches at 300 DPI
```

## Quick Reference: Format Selection

```
Vector graphics (charts, diagrams, flowcharts):
  → PDF (universal) or EPS (legacy LaTeX)

Photographs / microscopy / screenshots:
  → TIFF (lossless, preferred) or PNG

Supplementary / web:
  → PNG (lossless) or high-quality JPEG

Interactive:
  → SVG (web) or HTML (pyvis, plotly)

---

## 中文版本

### 使用场景
- 为特定期刊（IEEE、ACM、Nature、Science、Elsevier、Springer）格式化图表
- 投稿前检查图表尺寸、分辨率、字体要求
- 准备图表合规检查清单
- 在不同期刊格式要求之间转换图表
- 验证颜色模式和文件格式要求

### 工具库
```
pip install Pillow        # 图像处理和 DPI 验证
pip install matplotlib    # 用于 PDF/EPS 生成
```
```bash
# CLI 验证工具
brew install imagemagick   # macOS
apt install imagemagick    # Linux
```

### 代码模板说明
- **合规检查清单**：尺寸、分辨率、字体、颜色模式、文件格式、线宽、可读性等 10 项检查
- **DPI 验证脚本**：`check_dpi()` 自动检测图片 DPI 并给出重新导出建议
- **尺寸验证脚本**：`check_figure_size()` 比较实际尺寸与期刊要求

### 期刊规格速查
| 期刊 | 单栏宽度 | 双栏宽度 | 字体 | 最小字号 | 线条艺术分辨率 |
|------|---------|---------|------|---------|--------------|
| IEEE | 89mm | 182mm | Times New Roman | 6pt | 600 dpi |
| Nature | 89mm | 183mm | Arial/Helvetica | 6pt | 1000 dpi |
| Science | 87mm | 178mm | Helvetica/Arial | 5pt | 600 dpi |
| Elsevier | 90mm | 190mm | Arial/Helvetica/Courier | 6pt | 1000 dpi |
| Springer | 84mm | 174mm | Arial/Helvetica | 7pt | 1200 dpi |
| ACM | 89mm | 178mm | Times New Roman/Helvetica | 6pt | 300 dpi |

### 常见陷阱
1. **DPI 与 PPI 混淆**：DPI 用于印刷；PPI 用于屏幕。期刊要求的是印刷 DPI
2. **矢量格式无 DPI**：PDF/EPS/SVG 分辨率无关；DPI 仅适用于栅格图
3. **缩放后字号变化**：始终在最终打印尺寸下检查字号
4. **CMYK 色偏**：仅在期刊要求时从 RGB 转 CMYK；颜色可能偏移
5. **TIFF 压缩**：使用 LZW 压缩；避免 JPEG 压缩的 TIFF
6. **PDF 版本**：推荐 PDF 1.4+；避免 PDF 2.0 特性
7. **PDF 字体嵌入**：确保所有字体已嵌入（用 `pdffonts` 检查）
```
