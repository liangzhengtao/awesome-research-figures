# Statistical Visualization with Seaborn

## When to Use

- Creating statistical plots: distributions, correlations, regressions
- Visualizing dataset relationships with pair plots or heatmaps
- Generating publication-ready categorical plots (violin, strip, swarm)
- Comparing distributions across experimental conditions
- Exploratory data analysis for papers or supplementary materials

## Tools and Libraries

```
pip install seaborn matplotlib pandas numpy scipy
```

## Step-by-Step Instructions

### 1. Configure Seaborn for Publications

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# Publication-ready Seaborn theme
PUB_THEME = {
    'font.family': 'serif',
    'font.serif': ['Times New Roman', 'DejaVu Serif'],
    'font.size': 10,
    'axes.labelsize': 10,
    'axes.titlesize': 12,
    'xtick.labelsize': 9,
    'ytick.labelsize': 9,
    'legend.fontsize': 9,
    'figure.dpi': 300,
    'savefig.dpi': 600,
    'savefig.bbox': 'tight',
    'axes.linewidth': 0.8,
    'xtick.direction': 'in',
    'ytick.direction': 'in',
    'xtick.major.size': 4,
    'ytick.major.size': 4,
}

plt.rcParams.update(PUB_THEME)

# Colorblind-safe palette
PALETTE = sns.color_palette(['#0072B2', '#D55E00', '#009E73',
                              '#CC79A7', '#E69F00', '#56B4E9'])
sns.set_palette(PALETTE)
```

### 2. Journal-Specific Figure Sizes

```python
FIG_SINGLE = (3.5, 2.8)       # 89 mm
FIG_ONE_HALF = (5.0, 3.8)     # 127 mm
FIG_DOUBLE = (7.0, 4.5)       # 178 mm
```

## Code Templates

### Template 1: Publication-Ready Heatmap

```python
def plot_correlation_heatmap(df, method='pearson', annot=True,
                              filename='heatmap.pdf',
                              figsize=None, mask_upper=True):
    """
    Publication-quality correlation heatmap.

    Parameters
    ----------
    df : pd.DataFrame
        Input data with numeric columns.
    method : str
        Correlation method ('pearson', 'spearman', 'kendall').
    mask_upper : bool
        Whether to mask the upper triangle for clarity.
    """
    corr = df.corr(method=method)
    n = len(corr.columns)

    if figsize is None:
        figsize = (max(3.5, n * 0.6), max(2.8, n * 0.5))

    mask = np.triu(np.ones_like(corr, dtype=bool)) if mask_upper else None

    fig, ax = plt.subplots(figsize=figsize)
    cmap = sns.diverging_palette(220, 10, as_cmap=True)

    sns.heatmap(corr, mask=mask, cmap=cmap, center=0,
                vmin=-1, vmax=1, annot=annot, fmt='.2f',
                annot_kws={'size': 7 if n > 8 else 8},
                square=True, linewidths=0.5,
                cbar_kws={'shrink': 0.8, 'label': f'{method.capitalize()} Correlation'},
                ax=ax)

    ax.set_xticklabels(ax.get_xticklabels(), rotation=45, ha='right')
    fig.savefig(filename, format='pdf')
    plt.close(fig)
    print(f"Saved: {filename}")

# Usage
if __name__ == '__main__':
    np.random.seed(42)
    df = pd.DataFrame(np.random.randn(200, 6),
                      columns=['Metric A', 'Metric B', 'Metric C',
                               'Metric D', 'Metric E', 'Metric F'])
    plot_correlation_heatmap(df, filename='heatmap.pdf')
```

### Template 2: Pair Plot for Multivariate Analysis

```python
def plot_pair(df, hue_col, vars_list=None,
              filename='pairplot.pdf', height=2.0):
    """
    Publication-quality pair plot with marginal distributions.

    Parameters
    ----------
    df : pd.DataFrame
        Input data.
    hue_col : str
        Column name for color grouping.
    vars_list : list of str, optional
        Variables to plot. Defaults to all numeric except hue.
    """
    if vars_list is None:
        vars_list = [c for c in df.select_dtypes(include=[np.number]).columns
                     if c != hue_col]

    g = sns.pairplot(df, vars=vars_list, hue=hue_col,
                     palette=PALETTE[:df[hue_col].nunique()],
                     diag_kind='kde',
                     plot_kws={'alpha': 0.5, 's': 15,
                               'edgecolor': 'white', 'linewidth': 0.3},
                     diag_kws={'linewidth': 1.5, 'fill': True, 'alpha': 0.5},
                     height=height)

    g.figure.savefig(filename, format='pdf')
    plt.close(g.figure)
    print(f"Saved: {filename}")
```

### Template 3: Violin + Strip Plot Combination

```python
def plot_violin_strip(df, x, y, hue=None, filename='violin_strip.pdf',
                      figsize=FIG_ONE_HALF):
    """
    Combined violin plot with overlaid strip plot for individual data points.
    """
    fig, ax = plt.subplots(figsize=figsize)

    palette = PALETTE[:df[hue].nunique()] if hue else PALETTE[:1]

    sns.violinplot(data=df, x=x, y=y, hue=hue,
                   palette=palette, inner=None, alpha=0.3,
                   linewidth=0.8, cut=0, ax=ax)

    dodge = hue is not None
    sns.stripplot(data=df, x=x, y=y, hue=hue,
                  palette=palette, dodge=dodge,
                  size=3, alpha=0.6, jitter=0.15,
                  edgecolor='white', linewidth=0.3, ax=ax)

    # Fix legend duplicates
    handles, labels = ax.get_legend_handles_labels()
    n_levels = df[hue].nunique() if hue else 1
    ax.legend(handles[:n_levels], labels[:n_levels],
              framealpha=0.9, fontsize=9)

    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
    print(f"Saved: {filename}")

# Usage
if __name__ == '__main__':
    np.random.seed(42)
    groups = ['Control', 'Method A', 'Method B', 'Method C']
    conditions = ['Dataset 1', 'Dataset 2']
    rows = []
    for g in groups:
        for c in conditions:
            vals = np.random.normal(loc=groups.index(g) * 2, scale=1.5, size=30)
            for v in vals:
                rows.append({'Group': g, 'Condition': c, 'Score': v})
    df = pd.DataFrame(rows)
    plot_violin_strip(df, x='Group', y='Score', hue='Condition')
```

### Template 4: Regression Plot with Multiple Models

```python
def plot_regression_comparison(x, y_dict, xlabel, ylabel,
                                filename='regression.pdf',
                                figsize=FIG_SINGLE):
    """
    Plot multiple regression fits with confidence intervals.
    """
    fig, ax = plt.subplots(figsize=figsize)

    for i, (label, y) in enumerate(y_dict.items()):
        color = PALETTE[i % len(PALETTE)]
        ax.scatter(x, y, c=[color], s=12, alpha=0.4,
                   edgecolors='white', linewidths=0.2)

        # Lowess smoothing
        sns.regplot(x=x, y=y, scatter=False,
                    color=color, label=label,
                    line_kws={'linewidth': 1.5},
                    ci=95, ax=ax)

    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    ax.legend(framealpha=0.9)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 5: Distribution Comparison (KDE + Histogram)

```python
def plot_distribution_comparison(data_dict, xlabel, ylabel='Density',
                                  filename='distribution.pdf',
                                  figsize=FIG_SINGLE):
    """
    Overlaid KDE curves with subtle histograms.
    """
    fig, ax = plt.subplots(figsize=figsize)

    for i, (label, values) in enumerate(data_dict.items()):
        color = PALETTE[i % len(PALETTE)]
        sns.histplot(values, kde=True, stat='density',
                     color=color, alpha=0.2, linewidth=0,
                     bins=25, ax=ax)
        sns.kdeplot(values, color=color, linewidth=1.5,
                    label=label, ax=ax)

    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    ax.legend(framealpha=0.9)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 6: Categorical Bar Plot with Significance

```python
from scipy import stats

def plot_categorical_with_significance(df, x, y, pairs, hue=None,
                                        filename='categorical.pdf',
                                        figsize=FIG_ONE_HALF):
    """
    Bar or point plot with significance annotations (stars).
    """
    fig, ax = plt.subplots(figsize=figsize)

    sns.barplot(data=df, x=x, y=y, hue=hue,
                palette=PALETTE, capsize=0.1,
                errwidth=1, edgecolor='black', linewidth=0.5,
                alpha=0.8, ax=ax)

    # Add significance stars
    y_max = df[y].max()
    h = y_max * 0.05
    for i, (g1, g2) in enumerate(pairs):
        g1_vals = df[df[x] == g1][y]
        g2_vals = df[df[x] == g2][y]
        _, p = stats.mannwhitneyu(g1_vals, g2_vals)

        if p < 0.001:
            star = '***'
        elif p < 0.01:
            star = '**'
        elif p < 0.05:
            star = '*'
        else:
            star = 'ns'

        x1 = list(df[x].unique()).index(g1)
        x2 = list(df[x].unique()).index(g2)
        bar_y = y_max + h * (i + 1)
        ax.plot([x1, x1, x2, x2], [bar_y, bar_y + h * 0.3,
                bar_y + h * 0.3, bar_y],
                linewidth=0.8, color='black')
        ax.text((x1 + x2) / 2, bar_y + h * 0.35, star,
                ha='center', va='bottom', fontsize=8)

    ax.set_ylim(top=y_max + h * (len(pairs) + 1.5))
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

## Style Specifications

| Parameter | Recommended Value |
|-----------|-------------------|
| Font family | serif (Times New Roman) or sans-serif (Arial) |
| Font size (labels) | 10 pt |
| Font size (ticks) | 9 pt |
| Font size (annotation) | 8 pt |
| Line width (axes) | 0.8 pt |
| Line width (data) | 1.5 pt |
| Marker size | 3-5 pt |
| DPI (raster) | 300 for draft, 600 for submission |
| Color palette | Colorblind-safe (Wong 2011) |

## Common Pitfalls

1. **Seaborn styles override rcParams**: Call `sns.set_theme()` before `plt.rcParams.update()`
2. **Palette length mismatch**: Always check `nunique()` and cap palette accordingly
3. **Heatmap annot too crowded**: Reduce `annot_kws` font size when n > 10
4. **Violin plot with few data points**: Use `cut=0` to avoid extending beyond data range
5. **Strip plot jitter overlapping violin**: Set `alpha < 0.7` and `size <= 4`
6. **Significance annotations misaligned**: Calculate x-positions from actual category indices, not positions
7. **Legend duplicates in violin+strip**: Extract handles from only one layer

## Journal-Specific Tips

- **Nature/Science**: Prefer minimal grid lines; use `sns.despine()` for clean look
- **IEEE**: Use serif fonts; keep figure width at 3.5 in (single) or 7.16 in (double)
- **PLOS ONE**: Requires 300 dpi minimum; TIFF or EPS preferred
- **Cell**: Supports wider figures; Arial font required
- **General**: Always provide source data alongside figures when required by journal policy

---

## 中文版本

### 使用场景
- 创建统计图表：分布图、相关性图、回归图
- 用配对图（pair plot）或热力图可视化数据集关系
- 生成出版级分类图表（小提琴图、散点条带图、蜂群图）
- 比较不同实验条件下的分布
- 论文或补充材料的探索性数据分析

### 工具库
```
pip install seaborn matplotlib pandas numpy scipy
```

### 代码模板说明
- **出版主题配置**：通过 `plt.rcParams` 和 `sns.set_palette` 统一样式
- **模板 1**：相关性热力图（支持 Pearson/Spearman/Kendall，可隐藏上三角）
- **模板 2**：多变量配对图（`pairplot` + KDE 对角线）
- **模板 3**：小提琴图 + 散点条带图组合（展示个体数据点）
- **模板 4**：多模型回归拟合比较（带 LOWESS 平滑和置信区间）
- **模板 5**：分布比较（KDE 曲线 + 直方图叠加）
- **模板 6**：带显著性标注的分类柱状图（Mann-Whitney U 检验星号）

### 常见陷阱
1. **Seaborn 样式覆盖 rcParams**：在 `plt.rcParams.update()` 之前调用 `sns.set_theme()`
2. **调色板长度不匹配**：始终检查 `nunique()` 并限制调色板长度
3. **热力图标注过于拥挤**：当 n > 10 时减小 `annot_kws` 字号
4. **数据点少时小提琴图失真**：使用 `cut=0` 避免超出数据范围
5. **散点条带与小提琴重叠**：设置 `alpha < 0.7` 且 `size <= 4`
6. **显著性标注错位**：根据实际类别索引计算 x 位置
7. **小提琴+条带图图例重复**：仅从一个图层提取图例句柄
