# Technical Diagrams with TikZ

## When to Use

- Creating architecture diagrams, flowcharts, or neural network diagrams in LaTeX
- Building state machines, block diagrams, or system overviews
- Need pixel-perfect alignment with LaTeX document fonts
- Creating reusable diagram macros for a paper or thesis
- Drawing conceptual diagrams that integrate seamlessly with text

## Tools and Libraries

- LaTeX distribution (TeX Live, MiKTeX)
- Packages: `tikz`, `tikz-cd`, `tikz-network`, `tikzmark`

```latex
\usepackage{tikz}
\usetikzlibrary{
  arrows.meta, positioning, shapes.geometric, shapes.multipart,
  calc, fit, backgrounds, decorations.pathreplacing,
  chains, matrix, patterns, shadows.blur
}
```

## Step-by-Step Instructions

### 1. Configure TikZ Defaults

```latex
\tikzset{
  % Global styles
  every node/.style={
    font=\small,
    inner sep=2pt,
  },
  % Block style
  block/.style={
    rectangle, draw, minimum width=2cm, minimum height=0.8cm,
    fill=pubblue!15, line width=0.5pt, rounded corners=2pt,
    font=\small, align=center,
  },
  % Decision diamond
  decision/.style={
    diamond, draw, minimum width=1.5cm, minimum height=1cm,
    fill=puborange!15, line width=0.5pt,
    font=\small, align=center, aspect=1.5,
  },
  % Arrow style
  arrow/.style={
    -Stealth, line width=0.6pt, color=black!70,
  },
  % Dashed arrow
  dasharrow/.style={
    -Stealth, dashed, line width=0.5pt, color=black!50,
  },
  % Layer block (for neural networks)
  layer/.style={
    rectangle, draw, minimum width=0.4cm, minimum height=2.5cm,
    fill=#1!30, line width=0.5pt, rounded corners=1pt,
  },
  layer/.default=pubblue,
}

% Colors
\definecolor{pubblue}{HTML}{0072B2}
\definecolor{puborange}{HTML}{D55E00}
\definecolor{pubgreen}{HTML}{009E73}
\definecolor{pubpink}{HTML}{CC79A7}
```

## Code Templates

### Template 1: CNN Architecture Diagram

```latex
\begin{tikzpicture}[node distance=0.3cm]
  % Input
  \node[layer=pubblue, minimum width=0.8cm, minimum height=3cm] (input)
    {};
  \node[below=0.1cm of input, font=\scriptsize] {Input};
  \node[above=0.05cm of input, font=\tiny] {$224\times224\times3$};

  % Conv1
  \node[layer=puborange, right=0.4cm of input, minimum width=0.6cm,
        minimum height=2.5cm] (conv1) {};
  \node[below=0.1cm of conv1, font=\scriptsize] {Conv1};
  \node[above=0.05cm of conv1, font=\tiny] {$112\times112\times64$};

  % Pool1
  \node[layer=pubgreen, right=0.3cm of conv1, minimum width=0.4cm,
        minimum height=2cm] (pool1) {};
  \node[below=0.1cm of pool1, font=\scriptsize] {Pool1};
  \node[above=0.05cm of pool1, font=\tiny] {$56\times56\times64$};

  % Conv2
  \node[layer=puborange, right=0.3cm of pool1, minimum width=0.6cm,
        minimum height=1.6cm] (conv2) {};
  \node[below=0.1cm of conv2, font=\scriptsize] {Conv2};
  \node[above=0.05cm of conv2, font=\tiny] {$56\times56\times128$};

  % Pool2
  \node[layer=pubgreen, right=0.3cm of conv2, minimum width=0.4cm,
        minimum height=1.2cm] (pool2) {};
  \node[below=0.1cm of pool2, font=\scriptsize] {Pool2};

  % FC
  \node[layer=pubpink, right=0.3cm of pool2, minimum width=0.3cm,
        minimum height=0.8cm] (fc1) {};
  \node[below=0.1cm of fc1, font=\scriptsize] {FC};

  % Output
  \node[layer=pubpink, right=0.3cm of fc1, minimum width=0.3cm,
        minimum height=0.4cm] (output) {};
  \node[below=0.1cm of output, font=\scriptsize] {Output};

  % Arrows
  \draw[arrow] (input) -- (conv1);
  \draw[arrow] (conv1) -- (pool1);
  \draw[arrow] (pool1) -- (conv2);
  \draw[arrow] (conv2) -- (pool2);
  \draw[arrow] (pool2) -- (fc1);
  \draw[arrow] (fc1) -- (output);
\end{tikzpicture}
```

### Template 2: Transformer Block Diagram

```latex
\begin{tikzpicture}[
  node distance=0.5cm,
  attn/.style={block, fill=puborange!20, minimum width=3cm},
  ffn/.style={block, fill=pubblue!20, minimum width=3cm},
  norm/.style={block, fill=pubgreen!15, minimum width=3cm,
               minimum height=0.5cm},
]
  % Input
  \node[block, minimum width=3cm] (input) {Input Embedding};

  % Multi-Head Attention
  \node[attn, above=0.6cm of input] (mha) {Multi-Head Attention};
  \node[block, fill=none, draw=none, left=0.2cm of mha,
        font=\footnotesize, text width=1.5cm, align=center] (qkv)
    {$Q$, $K$, $V$};

  % Add & Norm
  \node[norm, above=0.3cm of mha] (norm1) {Add \& LayerNorm};

  % Feed Forward
  \node[ffn, above=0.3cm of norm1] (ffn) {Feed-Forward Network};

  % Add & Norm
  \node[norm, above=0.3cm of ffn] (norm2) {Add \& LayerNorm};

  % Output
  \node[block, above=0.3cm of norm2] (output) {Output};

  % Skip connections (residual)
  \draw[arrow] (input) -- (mha);
  \draw[arrow] (mha) -- (norm1);
  \draw[arrow] (norm1) -- (ffn);
  \draw[arrow] (ffn) -- (norm2);
  \draw[arrow] (norm2) -- (output);

  % Residual connections
  \draw[dasharrow] (input.east) -- ++(1,0) |- (norm1.east);
  \draw[dasharrow] (norm1.east) -- ++(0.8,0) |- (norm2.east);

  % Layer labels
  \draw[decorate, decoration={brace, amplitude=5pt, mirror},
        thick, puborange]
    ($(mha.west)+(-0.3,0)$) -- ($(norm1.west)+(-0.3,0)$)
    node[midway, left=8pt, font=\scriptsize] {Encoder Layer};
\end{tikzpicture}
```

### Template 3: System Architecture Overview

```latex
\begin{tikzpicture}[
  node distance=0.8cm and 1.2cm,
  component/.style={
    rectangle, draw, minimum width=2.5cm, minimum height=1cm,
    rounded corners=3pt, font=\small, align=center,
    line width=0.6pt,
  },
  db/.style={component, fill=pubblue!15},
  service/.style={component, fill=puborange!15},
  client/.style={component, fill=pubgreen!15},
  data/.style={component, fill=pubpink!15},
]

  % Layers
  \node[client] (web) {Web Client};
  \node[client, right=1.5cm of web] (mobile) {Mobile App};

  \node[service, below=1cm of $(web)!0.5!(mobile)$] (api)
    {API Gateway};
  \node[service, left=1.2cm of api] (auth) {Auth Service};
  \node[service, right=1.2cm of api] (ml) {ML Service};

  \node[db, below=1cm of auth] (userdb) {User DB};
  \node[db, below=1cm of api] (cache) {Redis Cache};
  \node[data, below=1cm of ml] (model) {Model Store};

  % Connections
  \draw[arrow] (web.south) -- (api.north);
  \draw[arrow] (mobile.south) -- (api.north);
  \draw[arrow] (api) -- (auth);
  \draw[arrow] (api) -- (ml);
  \draw[arrow] (auth.south) -- (userdb.north);
  \draw[arrow] (api.south) -- (cache.north);
  \draw[arrow] (ml.south) -- (model.north);

  % Background group
  \begin{scope}[on background layer]
    \node[draw, dashed, rounded corners=5pt, inner sep=10pt,
          fill=pubblue!3, fit=(api)(auth)(ml)] {};
    \node[above=2pt of $(auth.north)!0.5!(ml.north)$,
          font=\footnotesize\itshape, text=pubblue] {Backend Services};
  \end{scope}
\end{tikzpicture}
```

### Template 4: Algorithm Flowchart

```latex
\begin{tikzpicture}[node distance=0.6cm]
  \node[decision] (start) {Start};
  \node[block, below=0.6cm of start] (init) {Initialize\\parameters};
  \node[decision, below=0.6cm of init] (check) {Converged?};
  \node[block, below=0.6cm of check] (update) {Update\\weights};
  \node[block, right=1.5cm of check] (output) {Return\\results};

  \draw[arrow] (start) -- (init);
  \draw[arrow] (init) -- (check);
  \draw[arrow] (check) -- node[right, font=\scriptsize] {No} (update);
  \draw[arrow] (update.west) -| ++(-1.5,0) |- (check.west);
  \draw[arrow] (check.east) -- node[above, font=\scriptsize] {Yes} (output);
\end{tikzpicture}
```

## Style Specifications

| Element | Value |
|---------|-------|
| Node minimum width | 2–3 cm |
| Node minimum height | 0.6–1 cm |
| Rounded corners | 2–3 pt |
| Line width (edges) | 0.5–0.8 pt |
| Arrow tip | Stealth (or latex) |
| Font in nodes | \small (10pt) or \footnotesize (8pt) |
| Node inner sep | 2–4 pt |
| Node fill opacity | 15–25% |
| Dash pattern (residual) | dashed, 2pt on / 2pt off |

## Common Pitfalls

1. **Node positions drift**: Use `positioning` library with `above=of X` instead of `above of=X`
2. **Arrow tip size**: Set `>=Stealth[length=4pt]` globally
3. **Text overflow**: Use `text width=2cm` or `align=center` for wrapping
4. **Background layer**: Requires `\usetikzlibrary{backgrounds}` and `\begin{scope}[on background layer]`
5. **Brace decoration offset**: Use `amplitude=5pt` and add `inner sep` for clearance
6. **Font inconsistency**: Set font sizes explicitly; don't rely on document defaults
7. **Compilation time**: TikZ externalization helps: `\usetikzlibrary{external}\tikzexternalize`

## Journal-Specific Tips

- **IEEE**: Keep TikZ figures inside `\begin{figure}` with `\centering`; PDF output preferred
- **Springer**: Use `width=\columnwidth` scaling
- **Nature**: TikZ diagrams in PDF are accepted; match font to Helvetica if possible
- **Thesis**: Create reusable `\newcommand` macros for consistent diagrams across chapters
- **General**: Externalize TikZ to speed up compilation: `\tikzset{external/force remake}`
