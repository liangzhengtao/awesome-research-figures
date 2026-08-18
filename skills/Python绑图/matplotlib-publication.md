# Publication-Quality Matplotlib Figures

## When to Use

- Creating figures for academic papers using Python
- Generating line plots, bar charts, scatter plots, box plots, or violin plots for journal submission
- Need consistent, reproducible figure styling across a research project
- Preparing figures for IEEE, Nature, Science, Elsevier, or Springer journals

## Tools and Libraries

```
pip install matplotlib numpy scipy
```

## Step-by-Step Instructions

### 1. Set Up the Publication Style Environment

```python
import matplotlib
matplotlib.use('Agg')  # Non-interactive backend for reproducibility
import matplotlib.pyplot as plt
import numpy as np

# Global publication style
plt.rcParams.update({
    # Font settings
    'font.family': 'serif',
    'font.serif': ['Times New Roman', 'DejaVu Serif'],
    'font.size': 10,
    'mathtext.fontset': 'stix',

    # Axes settings
    'axes.labelsize': 10,
    'axes.titlesize': 12,
    'axes.linewidth': 0.8,
    'axes.unicode_minus': False,

    # Tick settings
    'xtick.labelsize': 9,
    'ytick.labelsize': 9,
    'xtick.direction': 'in',
    'ytick.direction': 'in',
    'xtick.major.size': 4,
    'ytick.major.size': 4,
    'xtick.minor.size': 2,
    'ytick.minor.size': 2,
    'xtick.major.width': 0.8,
    'ytick.major.width': 0.8,

    # Legend settings
    'legend.fontsize': 9,
    'legend.frameon': True,
    'legend.framealpha': 0.9,
    'legend.edgecolor': '0.8',

    # Figure settings
    'figure.dpi': 300,
    'savefig.dpi': 600,
    'savefig.bbox': 'tight',
    'savefig.pad_inches': 0.05,

    # Grid settings
    'grid.linewidth': 0.5,
    'grid.alpha': 0.3,
})
```

### 2. Journal-Specific Figure Sizes

```python
# Single-column figure (width ~3.5 inch / 89 mm)
FIG_SINGLE = (3.5, 2.8)

# 1.5-column figure (width ~5.0 inch / 127 mm)
FIG_ONE_HALF = (5.0, 3.8)

# Double-column figure (width ~7.0 inch / 178 mm)
FIG_DOUBLE = (7.0, 4.5)

# Nature single column (89 mm)
FIG_NATURE_SINGLE = (3.504, 2.628)

# Nature double column (183 mm)
FIG_NATURE_DOUBLE = (7.205, 5.404)

# IEEE single column (3.5 inch)
FIG_IEEE_SINGLE = (3.5, 2.8)

# IEEE double column (7.16 inch)
FIG_IEEE_DOUBLE = (7.16, 5.0)

# Science single column (3.42 inch)
FIG_SCIENCE_SINGLE = (3.42, 2.565)
```

### 3. Publication Color Palettes

```python
# Colorblind-safe palette (based on Wong 2011, Nature Methods)
COLORS_WONG = ['#0072B2', '#D55E00', '#009E73',
               '#CC79A7', '#E69F00', '#56B4E9',
               '#F0E442', '#000000']

# Pastel academic palette
COLORS_PASTEL = ['#4C72B0', '#DD8452', '#55A868',
                 '#C44E52', '#8172B3', '#937860',
                 '#DA8BC3', '#8C8C8C']

# High-contrast for grayscale printing
COLORS_GRAYSCALE = ['#000000', '#444444', '#777777',
                     '#AAAAAA', '#CCCCCC']

# Line styles for distinguishing in grayscale
LINE_STYLES = ['-', '--', '-.', ':']
MARKERS = ['o', 's', '^', 'D', 'v', 'p', 'h', '*']

def apply_colorblind_palette(ax, n_series):
    """Apply colorblind-safe colors and distinct markers."""
    for i, line in enumerate(ax.get_lines()):
        line.set_color(COLORS_WONG[i % len(COLORS_WONG)])
        line.set_marker(MARKERS[i % len(MARKERS)])
        line.set_linestyle(LINE_STYLES[i % len(LINE_STYLES)])
        line.set_markersize(5)
        line.set_linewidth(1.5)
```

## Code Templates

### Template 1: Line Plot with Error Bars

```python
def plot_line_with_error(x, y_mean, y_std, labels, xlabel, ylabel,
                         filename='line_plot.pdf', figsize=FIG_SINGLE):
    """Create a publication-quality line plot with shaded error regions."""
    fig, ax = plt.subplots(figsize=figsize)

    for i in range(len(labels)):
        color = COLORS_WONG[i % len(COLORS_WONG)]
        marker = MARKERS[i % len(MARKERS)]
        ax.plot(x, y_mean[i], color=color, marker=marker,
                markersize=5, linewidth=1.5, label=labels[i],
                markevery=max(1, len(x)//10))
        ax.fill_between(x, y_mean[i] - y_std[i],
                        y_mean[i] + y_std[i],
                        color=color, alpha=0.15)

    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    ax.legend(loc='best', framealpha=0.9)
    ax.minorticks_on()
    fig.savefig(filename, format='pdf')
    plt.close(fig)
    print(f"Saved: {filename}")

# Usage example
if __name__ == '__main__':
    x = np.linspace(0, 10, 50)
    y_mean = np.array([np.sin(x), np.cos(x)])
    y_std = np.array([np.abs(np.random.normal(0, 0.1, len(x))) for _ in range(2)])
    plot_line_with_error(x, y_mean, y_std,
                         labels=['Method A', 'Method B'],
                         xlabel='Epoch', ylabel='Accuracy')
```

### Template 2: Grouped Bar Chart

```python
def plot_grouped_bar(categories, data, labels, xlabel, ylabel,
                     filename='bar_chart.pdf', figsize=FIG_SINGLE):
    """Create grouped bar chart with error bars."""
    fig, ax = plt.subplots(figsize=figsize)
    n_groups = len(categories)
    n_bars = len(labels)
    bar_width = 0.8 / n_bars
    x = np.arange(n_groups)

    for i in range(n_bars):
        offset = (i - n_bars / 2 + 0.5) * bar_width
        color = COLORS_WONG[i % len(COLORS_WONG)]
        ax.bar(x + offset, data[i]['mean'], bar_width,
               yerr=data[i]['std'], label=labels[i],
               color=color, edgecolor='black', linewidth=0.5,
               capsize=2, error_kw={'linewidth': 0.8})

    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    ax.set_xticks(x)
    ax.set_xticklabels(categories)
    ax.legend(loc='best', framealpha=0.9)
    ax.set_ylim(bottom=0)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 3: Scatter Plot with Regression

```python
from scipy import stats

def plot_scatter_regression(x, y, xlabel, ylabel,
                            filename='scatter.pdf', figsize=FIG_SINGLE):
    """Scatter plot with linear regression and confidence interval."""
    fig, ax = plt.subplots(figsize=figsize)
    ax.scatter(x, y, c=COLORS_WONG[0], s=15, alpha=0.6,
               edgecolors='white', linewidths=0.3)

    # Linear regression
    slope, intercept, r_value, p_value, std_err = stats.linregress(x, y)
    x_line = np.linspace(x.min(), x.max(), 100)
    y_line = slope * x_line + intercept
    ax.plot(x_line, y_line, color=COLORS_WONG[1], linewidth=1.5,
            linestyle='--')

    # Confidence interval
    n = len(x)
    x_mean = np.mean(x)
    se = np.sqrt(np.sum((y - slope * x - intercept)**2) / (n - 2))
    ci = 1.96 * se * np.sqrt(1/n + (x_line - x_mean)**2 / np.sum((x - x_mean)**2))
    ax.fill_between(x_line, y_line - ci, y_line + ci,
                    color=COLORS_WONG[1], alpha=0.15)

    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    r2_text = f'$R^2 = {r_value**2:.3f}$, $p = {p_value:.2e}$'
    ax.annotate(r2_text, xy=(0.05, 0.95), xycoords='axes fraction',
                fontsize=9, verticalalignment='top',
                bbox=dict(boxstyle='round', facecolor='wheat', alpha=0.5))
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 4: Box Plot + Strip Plot

```python
def plot_box_strip(data, categories, xlabel, ylabel,
                   filename='boxplot.pdf', figsize=FIG_SINGLE):
    """Combined box plot with individual data points."""
    fig, ax = plt.subplots(figsize=figsize)

    positions = np.arange(1, len(categories) + 1)
    bp = ax.boxplot(data, positions=positions, widths=0.6,
                    patch_artist=True, showfliers=False)

    for i, box in enumerate(bp['boxes']):
        color = COLORS_WONG[i % len(COLORS_WONG)]
        box.set(facecolor=color, alpha=0.4, linewidth=1.0)
        bp['medians'][i].set(color='black', linewidth=1.5)

    for i, (d, pos) in enumerate(zip(data, positions)):
        jitter = np.random.normal(0, 0.04, len(d))
        ax.scatter(np.full_like(d, pos) + jitter, d,
                   c=COLORS_WONG[i % len(COLORS_WONG)],
                   s=10, alpha=0.6, zorder=5, edgecolors='white', linewidths=0.3)

    ax.set_xticks(positions)
    ax.set_xticklabels(categories)
    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

## Style Specifications

| Parameter | IEEE | Nature | Science | Elsevier |
|-----------|------|--------|---------|----------|
| Single column width | 89 mm (3.5 in) | 89 mm (3.5 in) | 87 mm (3.42 in) | 90 mm (3.54 in) |
| Double column width | 182 mm (7.16 in) | 183 mm (7.2 in) | 178 mm (7.0 in) | 190 mm (7.48 in) |
| Font | Times New Roman | Arial/Helvetica | Helvetica | Arial/Helvetica |
| Min font size in figure | 6 pt | 6 pt | 5 pt | 7 pt |
| Resolution (color) | 300 dpi | 300 dpi | 300 dpi | 300 dpi |
| Resolution (line art) | 600 dpi | 1000 dpi | 600 dpi | 1000 dpi |
| Color mode | RGB/CMYK | RGB | RGB | RGB/CMYK |
| Format | EPS/PDF/TIFF | PDF/EPS/TIFF | PDF/EPS/TIFF | EPS/PDF/TIFF |

## Common Pitfalls

1. **Font too small**: Minimum 6 pt after scaling; always check at final print size
2. **Low-resolution raster embedded in vector**: Export raster at 600+ dpi, or use vector (PDF/SVG)
3. **Inconsistent line widths**: Set `axes.linewidth` and all `linewidth` explicitly
4. **Colors indistinguishable in grayscale**: Test with `convert -colorspace Gray`
5. **Missing axis labels or units**: Always include units in parentheses, e.g., `Temperature (K)`
6. **Legend overlapping data**: Use `loc='best'` or place legend outside the axes
7. **Tick marks pointing outward**: Set `xtick.direction='in'` for publication style
8. **Figure not fitting column width**: Use journal-specific width constants above

## Journal-Specific Tips

### IEEE
- Prefer Times New Roman for all text in figures
- Use PDF or EPS format for vector graphics
- Minimum 300 dpi for halftones, 600 dpi for line art
- Number all figures sequentially (Fig. 1, Fig. 2, ...)

### Nature
- Arial or Helvetica preferred; minimum 6 pt font
- Provide source data for all figures
- Maximum width: 183 mm (double column) or 89 mm (single column)
- Use RGB color space

### Science
- Helvetica or Arial for labels
- Submit as PDF, EPS, or high-resolution TIFF
- Figure width: 3.42 in (single) or 7.0 in (double)
- Avoid red/green combinations for colorblind accessibility

### Elsevier
- Arial or Courier for figure text
- Minimum 6 pt font at final size
- TIFF, EPS, PDF, or MS Office formats accepted
- CMYK preferred for print journals

---

## 中文版本

### 使用场景
- 使用 Python 为学术论文创建出版级图表
- 生成折线图、柱状图、散点图、箱线图或小提琴图用于期刊投稿
- 需要在整个研究项目中保持一致、可复现的图表样式
- 为 IEEE、Nature、Science、Elsevier 或 Springer 期刊准备图表

### 工具库
```
pip install matplotlib numpy scipy
```

### 代码模板说明
- **全局出版样式设置**：通过 `plt.rcParams` 统一配置字体、坐标轴、刻度、图例等参数
- **期刊尺寸常量**：预定义单栏/双栏尺寸（Nature 89mm、IEEE 3.5in 等）
- **色盲友好调色板**：基于 Wong 2011（Nature Methods）的 8 色方案
- **模板 1**：带误差带的折线图（`fill_between`）
- **模板 2**：分组柱状图（带误差棒）
- **模板 3**：散点图 + 线性回归 + 置信区间
- **模板 4**：箱线图 + 散点叠加（strip plot）

### 常见陷阱
1. **字体过小**：缩放后最小 6 pt，务必在最终打印尺寸下检查
2. **矢量图中嵌入低分辨率栅格**：栅格图导出 600+ dpi，或使用矢量格式（PDF/SVG）
3. **线宽不一致**：显式设置 `axes.linewidth` 和所有 `linewidth`
4. **灰度打印下颜色不可区分**：用 `convert -colorspace Gray` 测试
5. **缺少坐标轴标签或单位**：单位用括号标注，如 `Temperature (K)`
6. **图例遮挡数据**：使用 `loc='best'` 或将图例放在坐标轴外
7. **刻度朝外**：设置 `xtick.direction='in'` 符合出版规范
8. **图表宽度不匹配栏宽**：使用上方的期刊专用宽度常量
