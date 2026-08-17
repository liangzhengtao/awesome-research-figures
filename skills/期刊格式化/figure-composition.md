# Multi-Panel Figure Composition

## When to Use

- Combining multiple subfigures into a single composite figure
- Creating figures with 2×2 grids, 1+2 layouts, or timeline arrangements
- Aligning axes, legends, and colorbars across subfigures
- Adding panel labels (a), (b), (c) consistently
- Preparing multi-panel figures for journal submission

## Tools and Libraries

```
pip install matplotlib Pillow
```

```bash
# Command-line tools
brew install imagemagick   # macOS / Linux
# apt install imagemagick  # Ubuntu/Debian
```

```r
# R
install.packages(c("patchwork", "cowplot", "ggpubr"))
```

## Step-by-Step Instructions

### 1. Plan the Layout First

Before coding, sketch the layout:

```
Common layouts:
  2×2 Grid:     [A][B]     ← Standard for comparisons
                 [C][D]

  1+2 Stack:     [  A  ]   ← One main plot + two details
                 [B][C]

  3×1 Row:       [A][B][C] ← Three equal plots

  Timeline:      [A]→[B]→[C]→[D]  ← Sequential process

  Sidebar:       [A][B]    ← Main plot with marginal distributions
                 [C][D]      (A=main, B=right marginal, C=bottom marginal)
```

### 2. Panel Label Convention

```
Label position: upper-left corner of each panel
Label format:   (a), (b), (c), ... or a., b., c., ...
Label style:    bold, slightly larger than body text
Label offset:   inside the axes, with small padding
```

## Code Templates

### Template 1: 2×2 Grid with Matplotlib

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams.update({
    'font.family': 'serif',
    'font.serif': ['Times New Roman', 'DejaVu Serif'],
    'font.size': 10,
    'axes.labelsize': 10,
    'axes.titlesize': 11,
    'figure.dpi': 300,
    'savefig.dpi': 600,
    'savefig.bbox': 'tight',
})

COLORS = ['#0072B2', '#D55E00', '#009E73', '#CC79A7']

def add_panel_label(ax, label, x=-0.12, y=1.08):
    """Add a bold panel label (a), (b), etc."""
    ax.text(x, y, f'({label})', transform=ax.transAxes,
            fontsize=12, fontweight='bold', va='top', ha='left')

def create_2x2_grid(data_dict, filename='figure_2x2.pdf'):
    """
    Standard 2×2 grid layout.

    Parameters
    ----------
    data_dict : dict with keys 'a', 'b', 'c', 'd', each containing
                plot function and data.
    """
    fig, axes = plt.subplots(2, 2, figsize=(7.16, 5.5))
    labels = ['a', 'b', 'c', 'd']

    for ax, label in zip(axes.flat, labels):
        # Placeholder: replace with actual plotting
        add_panel_label(ax, label)

    # Shared formatting
    for ax in axes.flat:
        ax.minorticks_on()
        ax.spines['top'].set_visible(False)
        ax.spines['right'].set_visible(False)

    fig.tight_layout(pad=0.5)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
    print(f"Saved: {filename}")

# Usage with real data
def plot_2x2_example(filename='figure_2x2.pdf'):
    np.random.seed(42)
    fig, axes = plt.subplots(2, 2, figsize=(7.16, 5.5))

    # (a) Line plot
    ax = axes[0, 0]
    x = np.linspace(0, 10, 50)
    for i, c in enumerate(COLORS[:3]):
        ax.plot(x, np.sin(x + i * 0.5), color=c, linewidth=1.5,
                label=f'Series {i+1}')
    ax.set_xlabel('Time (s)')
    ax.set_ylabel('Amplitude')
    ax.legend(fontsize=8, framealpha=0.9)
    add_panel_label(ax, 'a')

    # (b) Scatter plot
    ax = axes[0, 1]
    for i, c in enumerate(COLORS[:3]):
        cx, cy = np.random.randn(2, 30) * 0.5 + i * 1.5
        ax.scatter(cx, cy, c=c, s=20, alpha=0.6, label=f'Group {i+1}')
    ax.set_xlabel('Feature 1')
    ax.set_ylabel('Feature 2')
    ax.legend(fontsize=8, framealpha=0.9)
    add_panel_label(ax, 'b')

    # (c) Bar chart
    ax = axes[1, 0]
    methods = ['Method A', 'Method B', 'Method C', 'Baseline']
    values = [0.85, 0.82, 0.88, 0.75]
    bars = ax.bar(methods, values, color=COLORS[:4], edgecolor='black',
                  linewidth=0.5, width=0.6)
    ax.set_ylabel('F1 Score')
    ax.set_ylim(0, 1.0)
    add_panel_label(ax, 'c')

    # (d) Heatmap
    ax = axes[1, 1]
    data = np.random.rand(5, 5)
    im = ax.imshow(data, cmap='RdYlGn', vmin=0, vmax=1)
    cbar = fig.colorbar(im, ax=ax, shrink=0.8)
    cbar.set_label('Score', fontsize=9)
    ax.set_xticks(range(5))
    ax.set_yticks(range(5))
    add_panel_label(ax, 'd')

    # Global formatting
    for ax in axes.flat:
        ax.spines['top'].set_visible(False)
        ax.spines['right'].set_visible(False)

    fig.tight_layout(pad=0.5)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
    print(f"Saved: {filename}")

if __name__ == '__main__':
    plot_2x2_example()
```

### Template 2: 1+2 Layout (Main + Two Insets)

```python
def create_1plus2_layout(filename='figure_1plus2.pdf'):
    """
    One large plot on top, two smaller plots on bottom.
    """
    fig = plt.figure(figsize=(7.16, 6.0))
    gs = fig.add_gridspec(2, 2, height_ratios=[1.2, 1], hspace=0.35, wspace=0.3)

    ax_main = fig.add_subplot(gs[0, :])  # Top: spans both columns
    ax_left = fig.add_subplot(gs[1, 0])   # Bottom-left
    ax_right = fig.add_subplot(gs[1, 1])  # Bottom-right

    # Main plot
    np.random.seed(42)
    x = np.linspace(0, 100, 200)
    ax_main.plot(x, np.cumsum(np.random.randn(200)), color=COLORS[0],
                 linewidth=1.5)
    ax_main.set_xlabel('Time Step')
    ax_main.set_ylabel('Cumulative Reward')
    ax_main.set_title('Training Progress', fontsize=12)
    add_panel_label(ax_main, 'a')

    # Bottom-left
    data_a = np.random.normal(0.85, 0.05, 100)
    data_b = np.random.normal(0.78, 0.08, 100)
    ax_left.boxplot([data_a, data_b], labels=['Ours', 'Baseline'],
                    widths=0.5)
    ax_left.set_ylabel('Accuracy')
    add_panel_label(ax_left, 'b')

    # Bottom-right
    categories = ['Cat A', 'Cat B', 'Cat C', 'Cat D']
    values = [0.92, 0.87, 0.95, 0.89]
    ax_right.barh(categories, values, color=COLORS[:4],
                  edgecolor='black', linewidth=0.5, height=0.5)
    ax_right.set_xlabel('Score')
    add_panel_label(ax_right, 'c')

    for ax in [ax_main, ax_left, ax_right]:
        ax.spines['top'].set_visible(False)
        ax.spines['right'].set_visible(False)

    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 3: Timeline / Sequential Layout

```python
def create_timeline_layout(filename='timeline.pdf'):
    """
    Horizontal sequence of plots showing progression.
    """
    fig, axes = plt.subplots(1, 4, figsize=(7.16, 2.2), sharey=True)
    labels = ['Epoch 1', 'Epoch 10', 'Epoch 50', 'Epoch 100']
    panel_labels = ['a', 'b', 'c', 'd']
    np.random.seed(42)

    for ax, title, plabel, noise in zip(axes, labels, panel_labels,
                                         [0.8, 0.5, 0.2, 0.1]):
        # Simulated decision boundary plots
        xx, yy = np.meshgrid(np.linspace(-3, 3, 100), np.linspace(-3, 3, 100))
        Z = np.sign(xx + np.random.randn(*xx.shape) * noise)
        ax.contourf(xx, yy, Z, levels=[-1, 0, 1],
                    colors=[COLORS[0] + '40', COLORS[1] + '40']], alpha=0.7)
        ax.set_title(title, fontsize=9)
        ax.set_xticks([])
        ax.set_yticks([])
        add_panel_label(ax, plabel, y=1.05)

    fig.tight_layout(pad=0.3)
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 4: Using ImageMagick for Composition

```bash
#!/bin/bash
# compose_figures.sh — Combine pre-rendered panels

# 2×2 grid
montage fig_a.png fig_b.png fig_c.png fig_d.png \
  -tile 2x2 -geometry +10+10 -border 0 \
  -density 600 figure_2x2.pdf

# Horizontal strip
convert +append fig_a.png fig_b.png fig_c.png \
  -density 600 figure_strip.pdf

# Vertical stack
convert -append fig_a.png fig_b.png \
  -density 600 figure_stack.pdf

# Add labels using ImageMagick
convert figure_2x2.pdf \
  -font Times-New-Roman -pointsize 14 -gravity NorthWest \
  -annotate +10+10 "(a)" \
  -annotate +360+10 "(b)" \
  -annotate +10+400 "(c)" \
  -annotate +360+400 "(d)" \
  figure_2x2_labeled.pdf
```

### Template 5: R Multi-Panel with patchwork

```r
library(ggplot2)
library(patchwork)

create_multipanel_r <- function(filename = "figure_r.pdf") {
  p1 <- ggplot(mtcars, aes(wt, mpg)) + geom_point() + theme_minimal()
  p2 <- ggplot(mtcars, aes(factor(cyl), mpg)) + geom_boxplot() + theme_minimal()
  p3 <- ggplot(mtcars, aes(mpg)) + geom_histogram(bins = 15) + theme_minimal()
  p4 <- ggplot(mtcars, aes(disp, hp)) + geom_point() + theme_minimal()

  combined <- (p1 + p2) / (p3 + p4) +
    plot_annotation(tag_levels = 'a',
                    tag_prefix = '(',
                    tag_suffix = ')',
                    theme = theme(
                      plot.tag = element_text(face = 'bold', size = 14)
                    )) +
    plot_layout(guides = 'collect')

  ggsave(filename, combined, width = 7.16, height = 6, dpi = 600)
}
```

### Template 6: LaTeX subfigure Composition

```latex
\begin{figure*}[t]
  \centering
  \begin{subfigure}[b]{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{fig_a.pdf}
    \caption{Line plot comparison.}\label{fig:main_a}
  \end{subfigure}
  \hfill
  \begin{subfigure}[b]{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{fig_b.pdf}
    \caption{Scatter plot results.}\label{fig:main_b}
  \end{subfigure}

  \vspace{0.5em}

  \begin{subfigure}[b]{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{fig_c.pdf}
    \caption{Bar chart comparison.}\label{fig:main_c}
  \end{subfigure}
  \hfill
  \begin{subfigure}[b]{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{fig_d.pdf}
    \caption{Heatmap analysis.}\label{fig:main_d}
  \end{subfigure}

  \caption{Multi-panel figure with four subfigures.}\label{fig:main}
\end{figure*}
```

## Style Specifications

| Element | Value |
|---------|-------|
| Panel label | Bold, 11–12 pt, inside axes upper-left |
| Label format | (a), (b), (c) or a., b., c. |
| Spacing (hspace) | 0.3–0.5 |
| Spacing (wspace) | 0.3–0.5 |
| Shared axes | Use `sharex=True` or `sharey=True` |
| Shared legend | `fig.legend()` or `plot_layout(guides='collect')` |
| Shared colorbar | `fig.colorbar(mappable, ax=[ax1, ax2, ...])` |
| Figure width | Match journal column width (see journal-specs.md) |

## Common Pitfalls

1. **Inconsistent axis scales**: Use `sharex`/`sharey` when comparing same metric
2. **Labels not at consistent position**: Use the same `add_panel_label` function everywhere
3. **Legend duplication**: Collect legends to figure level: `fig.legend()`
4. **Tight layout issues**: Use `constrained_layout=True` instead of `tight_layout()` for complex layouts
5. **Panel (a) label not bold**: Set `fontweight='bold'` explicitly
6. **Colorbar misalignment**: Share colorbar via `fig.colorbar(im, ax=axes.ravel().tolist())`
7. **Subfigure reference in LaTeX**: Use `\subref{fig:main_a}` for (a) references

## Journal-Specific Tips

- **Nature**: Subfigures labeled (a), (b), ... in bold; max 8 display items total
- **IEEE**: Use `subfig` or `subcaption` package; single-column figures for IEEEtran
- **Science**: Combined figures count as one figure; total width 7.0 in max
- **Elsevier**: Use `subfig` package; `\begin{figure*}` for double-column
- **General**: Always export at final composition size; do not resize after composition
