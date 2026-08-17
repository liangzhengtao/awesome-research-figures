# Data Visualization with PGFPlots

## When to Use

- Creating figures directly in LaTeX documents for consistent fonts
- Need vector graphics with perfect font matching
- Generating line plots, bar charts, scatter plots in LaTeX
- Creating 3D surface plots or contour plots
- Working with LaTeX-only workflows (no external image dependencies)

## Tools and Libraries

- LaTeX distribution (TeX Live, MiKTeX)
- Packages: `pgfplots`, `tikz`, `pgfplotstable`

```latex
\usepackage{pgfplots}
\pgfplotsset{compat=1.18}
\usepgfplotslibrary{groupplots, statistics, fillbetween}
```

## Step-by-Step Instructions

### 1. Configure PGFPlots Defaults for Publications

```latex
\pgfplotsset{
  % Global publication style
  every axis/.style={
    width=0.45\textwidth,           % Adjust per journal
    height=0.35\textwidth,
    scale only axis=true,
    % Axis lines
    axis lines=left,
    axis line style={line width=0.6pt},
    % Ticks
    tick align=outside,
    tick style={line width=0.4pt, color=black},
    minor tick num=1,
    % Labels
    label style={font=\small},
    tick label style={font=\footnotesize},
    legend style={
      font=\footnotesize,
      draw=none,
      fill=white,
      fill opacity=0.9,
      /tikz/every even column/.append style={column sep=5pt},
    },
    % Grid
    grid=major,
    grid style={line width=0.2pt, draw=gray!20},
    % Colors
    cycle list name=color list,
  },
}

% Publication color cycle
\definecolor{pubblue}{HTML}{0072B2}
\definecolor{puborange}{HTML}{D55E00}
\definecolor{pubgreen}{HTML}{009E73}
\definecolor{pubpink}{HTML}{CC79A7}
\definecolor{pubyellow}{HTML}{E69F00}
\definecolor{publightblue}{HTML}{56B4E9}

\pgfplotscreateplotcyclelist{pubcycle}{
  {pubblue, mark=*, mark size=1.5pt, line width=1pt},
  {puborange, mark=square*, mark size=1.5pt, line width=1pt},
  {pubgreen, mark=triangle*, mark size=2pt, line width=1pt},
  {pubpink, mark=diamond*, mark size=1.5pt, line width=1pt},
  {pubyellow, mark=pentagon*, mark size=2pt, line width=1pt},
  {publightblue, mark=otimes*, mark size=2pt, line width=1pt},
}
```

## Code Templates

### Template 1: Line Plot with Error Bars

```latex
\begin{tikzpicture}
\begin{axis}[
  cycle list name=pubcycle,
  xlabel={Epoch},
  ylabel={Accuracy (\%)},
  xmin=0, xmax=100,
  ymin=60, ymax=100,
  legend pos=south east,
  legend columns=1,
]
% Method A
\addplot+[error bars/.cd, y dir=both, y explicit]
  table[x=epoch, y=mean, y error=std] {
    epoch  mean  std
    10     72.3  1.2
    20     81.5  0.9
    30     86.2  0.7
    40     89.1  0.5
    50     91.0  0.4
    60     92.3  0.3
    70     93.1  0.3
    80     93.8  0.2
    90     94.2  0.2
    100    94.5  0.2
  };
  \addlegendentry{Method A}

% Method B
\addplot+[error bars/.cd, y dir=both, y explicit]
  table[x=epoch, y=mean, y error=std] {
    epoch  mean  std
    10     68.1  1.5
    20     77.8  1.1
    30     83.5  0.8
    40     87.0  0.6
    50     89.5  0.5
    60     90.8  0.4
    70     91.8  0.3
    80     92.5  0.3
    90     93.0  0.2
    100    93.3  0.2
  };
  \addlegendentry{Method B}

% Method C (baseline)
\addplot+[dashed, error bars/.cd, y dir=both, y explicit]
  table[x=epoch, y=mean, y error=std] {
    epoch  mean  std
    10     65.0  2.0
    20     73.2  1.5
    30     78.5  1.0
    40     82.0  0.8
    50     84.5  0.6
    60     86.0  0.5
    70     87.2  0.4
    80     88.0  0.3
    90     88.5  0.3
    100    88.8  0.3
  };
  \addlegendentry{Baseline}
\end{axis}
\end{tikzpicture}
```

### Template 2: Grouped Bar Chart

```latex
\begin{tikzpicture}
\begin{axis}[
  ybar,
  bar width=5pt,
  width=0.5\textwidth,
  height=0.35\textwidth,
  xlabel={Dataset},
  ylabel={F1 Score},
  symbolic x coords={Set A, Set B, Set C, Set D},
  xtick=data,
  x tick label style={rotate=0},
  ymin=0, ymax=1.0,
  legend pos=north west,
  legend style={font=\footnotesize, draw=none},
  nodes near coords,
  nodes near coords style={font=\tiny, anchor=south},
  every node near coord/.append style={rotate=90, anchor=west},
  enlarge x limits=0.2,
]
\addplot[fill=pubblue, draw=pubblue!80!black] coordinates {
  (Set A, 0.85) (Set B, 0.78) (Set C, 0.91) (Set D, 0.83)
};
\addlegendentry{Model 1}

\addplot[fill=puborange, draw=puborange!80!black] coordinates {
  (Set A, 0.82) (Set B, 0.80) (Set C, 0.88) (Set D, 0.86)
};
\addlegendentry{Model 2}

\addplot[fill=pubgreen, draw=pubgreen!80!black] coordinates {
  (Set A, 0.79) (Set B, 0.82) (Set C, 0.85) (Set D, 0.89)
};
\addlegendentry{Model 3}
\end{axis}
\end{tikzpicture}
```

### Template 3: Scatter Plot with Regression

```latex
\begin{tikzpicture}
\begin{axis}[
  xlabel={Predicted Value},
  ylabel={Actual Value},
  width=0.4\textwidth,
  height=0.35\textwidth,
  grid=major,
]
% Scatter points
\addplot[only marks, mark=*, mark size=1pt, pubblue, opacity=0.6]
  table {
    x    y
    1.2  1.1  2.5  2.8  3.1  3.0  4.0  4.3
    5.2  4.9  6.0  6.2  7.1  6.8  8.0  8.5
    2.0  1.8  3.5  3.2  4.8  5.0  5.5  5.8
    6.5  6.0  7.5  7.2  8.5  8.0  9.0  9.3
  };

% Regression line
\addplot[puborange, line width=1pt, domain=0:10, dashed]
  {0.95 * x + 0.2};
  \addlegendentry{$y = 0.95x + 0.2$, $R^2 = 0.97$}

% y = x reference line
\addplot[gray, line width=0.5pt, dotted, domain=0:10]
  {x};
\end{axis}
\end{tikzpicture}
```

### Template 4: 3D Surface Plot

```latex
\begin{tikzpicture}
\begin{axis}[
  width=0.5\textwidth,
  height=0.4\textwidth,
  view={135}{30},
  xlabel=$x$,
  ylabel=$y$,
  zlabel={$f(x,y)$},
  colormap/viridis,
  mesh/ordering=y varies,
  shader=interp,
  colorbar,
  colorbar style={
    ylabel={Value},
    width=3mm,
  },
]
\addplot3[
  surf,
  domain=-2:2,
  domain y=-2:2,
  samples=40,
  samples y=40,
] {exp(-x^2 - y^2) * cos(deg(2*x)) * sin(deg(2*y))};
\end{axis}
\end{tikzpicture}
```

### Template 5: Box Plot with PGFPlots Statistics

```latex
\begin{tikzpicture}
\begin{axis}[
  boxplot/draw direction=y,
  width=0.45\textwidth,
  height=0.35\textwidth,
  xlabel={Method},
  ylabel={Score},
  xtick={1,2,3,4},
  xticklabels={Baseline, Model A, Model B, Model C},
  ymin=0, ymax=1.0,
]
\addplot+[boxplot prepared={
    lower whisker=0.52, lower quartile=0.68,
    median=0.78, upper quartile=0.85,
    upper whisker=0.92,
  }, fill=pubblue!30, draw=pubblue] coordinates {};
\addplot+[boxplot prepared={
    lower whisker=0.58, lower quartile=0.72,
    median=0.82, upper quartile=0.88,
    upper whisker=0.95,
  }, fill=puborange!30, draw=puborange] coordinates {};
\addplot+[boxplot prepared={
    lower whisker=0.61, lower quartile=0.75,
    median=0.85, upper quartile=0.90,
    upper whisker=0.97,
  }, fill=pubgreen!30, draw=pubgreen] coordinates {};
\addplot+[boxplot prepared={
    lower whisker=0.55, lower quartile=0.70,
    median=0.80, upper quartile=0.86,
    upper whisker=0.93,
  }, fill=pubpink!30, draw=pubpink] coordinates {};
\end{axis}
\end{tikzpicture}
```

## Style Specifications

| Parameter | IEEE | Nature | Springer |
|-----------|------|--------|----------|
| Figure width (single) | 8.5cm | 89mm | 84mm |
| Figure width (double) | 17.5cm | 183mm | 174mm |
| Font size in figure | \scriptsize (6pt) | \footnotesize (8pt) | \footnotesize (8pt) |
| Line width (data) | 0.8pt | 1pt | 0.8pt |
| Line width (axis) | 0.4pt | 0.5pt | 0.4pt |
| Mark size | 1.5pt | 2pt | 1.5pt |

## Common Pitfalls

1. **Compilation errors from special characters**: Escape `%`, `_`, `&` in table data
2. **Legend overlapping data**: Use `legend pos={north west}` or `legend style={at={(0.02,0.98)}}`
3. **Tick labels too small**: Scale with `tick label style={font=\footnotesize}`
4. **Color not printing well**: Use CMYK for print journals: `\selectcolormodel{cmyk}`
5. **3D plots too slow**: Reduce `samples` to 20-30 for draft, increase to 50+ for final
6. **Axis limits cutting data**: Add `enlarge x limits=0.05` for padding
7. **Missing compat version**: Always include `\pgfplotsset{compat=1.18}` to avoid warnings

## Journal-Specific Tips

- **IEEE**: Use `\usepackage[caption=false]{subfig}` for subfigures
- **Springer**: Use `width=\columnwidth` to match column exactly
- **Elsevier**: `\begin{figure*}` for double-width figures
- **Nature**: PDF figures from PGFPlots work perfectly in LaTeX submissions
- **General**: Compile with `pdflatex` or `lualatex` for best PGFPlots support
